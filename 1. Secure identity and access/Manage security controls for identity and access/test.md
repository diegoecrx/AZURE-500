# AZ-500: Secure Identity and Access – Smart Review

This document consolidates and reviews every major topic (“module”) within the **Manage security controls for identity and access** learning module. Each section summarizes key concepts and includes focused tips tailored to the AZ-500 exam. All information is drawn from the official Microsoft Learn content. 0

---

## 1. Secure Microsoft Entra Users and Password Controls

**Summary**  
Managing user accounts and passwords in Microsoft Entra ID (formerly Azure AD) is foundational. This includes creating and maintaining user objects, enforcing password policies, and requiring strong authentication. Key elements:

- **User Provisioning**  
  - Manual vs. bulk creation (CSV import, PowerShell).  
  - Assigning directory roles (User Administrator, Global Administrator) judiciously.  
  - Delegating user administration through scoped roles.

- **Password Protection**  
  - Configuring custom banned password lists and enforcing lockout policy.  
  - Enabling smart lockout to reduce brute-force risk.  
  - Enforcing self-service password reset (SSPR) with proper registration (2+ authentication methods).

- **Multifactor Authentication (MFA) Registration**  
  - Require MFA registration at first sign-in.  
  - Use Conditional Access to enforce MFA only when sign-in risk or location risk is high.  
  - Understand default MFA methods: text/SMS, phone call, Microsoft Authenticator push.

**Smart Exam Tips**  
1. **MFA Licensing Requirements**  
   - MFA per-user options are free, but risk-based MFA requires P2 (Identity Protection).  
   - Know which Conditional Access controls (e.g., “Require multifactor authentication”) demand P1/P2.  
2. **Password Protection Scope**  
   - Custom banned password lists apply only to Windows Server AD with Azure AD Password Protection agent (P1/P2).  
   - Built-in global banned password list protects cloud accounts even without on-premises integration.  
3. **User Administrator vs Global Administrator**  
   - User Administrator can manage all non-admin users and reset passwords, but cannot elevate roles.  
   - Global Administrator has full tenant control—assign sparingly.  
4. **SSPR Prerequisites**  
   - Self-service password reset for cloud-only users requires at least three registered authentication methods per user to unlock high-risk scenarios.  
5. **Delegated Administration**  
   - Use Privileged Access Groups or PIM to assign scoped administration (e.g., “User Administrator” only for a specific group).  
6. **Smart Lockout Behavior**  
   - Understand lockout threshold (10 failed attempts by default) and unlock duration.  
   - Know how to monitor “Account lockout” events in sign-in logs.

---

## 2. Secure Microsoft Entra Groups

**Summary**  
Groups simplify access management by offering collective assignment of licenses and permissions. Key subtopics:

- **Group Types**  
  - **Security Groups**: Control access to resources (Azure RBAC, Office 365 apps).  
  - **Microsoft 365 Groups**: Provide collaboration space (SharePoint, Teams, Outlook).  
  - **Dynamic Groups**: Query-based membership (e.g., all users in “Sales” OU).

- **Group-Based Licensing**  
  - Assign Microsoft 365/E5 licenses at the group level to automate license provisioning.  
  - Ensure dynamic membership rules include/exclude based on department, country, or job title.

- **Privileged Groups**  
  - Identify high-impact groups (e.g., “Global Administrators,” “Directory Readers”).  
  - Protect membership: require MFA, PIM-enforced approval, and access reviews.

- **Ownership and Delegation**  
  - Assign group owners to manage membership.  
  - Enforce expiration policies on guest group memberships (requires P2).

**Smart Exam Tips**  
1. **Dynamic Group Rule Syntax**  
   - Practice simple rules: `(user.department -eq "Sales")` or `(user.country -eq "BR")`.  
   - Know attribute types (string vs. integer) and supported operators.  
2. **Azure AD Roles vs Group Assignment**  
   - Understand difference: assigning a user to “Global Administrators” group does not grant that role—must assign role via “Roles and administrators.”  
3. **Group-Based Licensing Limitations**  
   - Certain license types (e.g., Azure AD Premium P2) cannot be assigned via group licensing; require direct assignment or group license feature enabled.  
4. **Protecting Privileged Groups**  
   - Use “Eligible” assignments in PIM for privileged roles rather than permanent membership.  
   - Review “Access reviews” for group owners every 30/60 days.  
5. **Guest User Expiration Policy**  
   - Only available in Azure AD P2.  
   - Configure from “Entitlement management” or “Access reviews” blade.  
6. **Renaming Groups**  
   - NOTE: Changing a group’s displayName does not affect its mailNickName or objectId.  
   - Examine how changes propagate for syncing with on-premises AD.

---

## 3. Manage External Identities

**Summary**  
External identities let organizations collaborate with business partners and customers securely. Main areas:

- **B2B Collaboration**  
  - Invite guests via email; they authenticate with their own identity provider.  
  - Limit guest access: configure “Collaboration restrictions” to restrict domains.  
  - Use “Cross-tenant access settings” to define inbound/outbound trust.

- **B2C (Business to Consumer)**  
  - Customizable identity experiences for customer apps.  
  - Support for social identity providers (Google, Facebook) and local accounts.  
  - Configure user flows (sign-up, sign-in, password reset) and custom policies for advanced scenarios.

- **Guest User Security**  
  - Enforce Conditional Access for guests: require MFA or compliant device.  
  - Block legacy authentication for external users.  
  - Restrict directory browsing (“Guests can’t see other directory users”).

- **External Collaboration Settings**  
  - Set default “Invitation redemption” (redeem only by invited email).  
  - Limit external user permissions (via “External collaboration settings” blade).

**Smart Exam Tips**  
1. **Guest vs. Member Account**  
   - MEMBERS are internal users; GUESTS have “UserType=Guest.”  
   - Conditional Access targeting can differentiate by `user.userType -eq "Guest"`.  
2. **B2B Inbound/Outbound Controls**  
   - Use “Cross-tenant access settings” rather than legacy “B2B collaboration policy.”  
   - Be prepared to configure “Trust settings” per specific partner tenant.  
3. **SSO Considerations for B2C**  
   - Custom domains (e.g., `login.contoso.com`) require creating a “Branding” profile and verifying domain DKIM/DMARC.  
   - For “Custom policies” (Identity Experience Framework), know file structure (TrustFrameworkBase.xml, etc.).  
4. **Limiting Guest Access**  
   - Azure AD P2 required for “Manage external collaboration settings.”  
   - Monitor “Invitation redemption events” in audit logs; they appear as “InvitationCreated” and “InvitationRedeemed.”  
5. **Social Identity Provider Claims**  
   - Map claims (email, name) from Facebook/Google to Azure AD B2C attributes.  
   - Be ready to write a simple “ClaimsTransformations” rule snippet.  
6. **Re-invite Flow**  
   - Understand how to re-send invitations and revoke guest access using the “Reset Password” link in Azure AD.

---

## 4. Microsoft Entra Identity Protection

**Summary**  
Identity Protection detects potential vulnerabilities and automates risk-based responses using machine-learning signals. Core components:

- **Risk Events and Detection**  
  - **User risk**: Low, medium, high based on compromised credentials, atypical travel, anonymous IP.  
  - **Sign-in risk**: Determined at each sign-in (impossible travel, unfamiliar sign-in properties, malware).  
  - View “Risk detection” reports in the Azure portal.

- **Risk Policies Configuration**  
  - **User Risk Policy**: Block or force password reset for users with medium/high risk.  
  - **Sign-in Risk Policy**: Require MFA (or block) based on detected sign-in risk level.  
  - **MFA Registration Policy**: Enforce user registration if not previously configured.

- **Remediation Flows**  
  - Automatic block or require password change/MFA.  
  - “Actions” can be integrated with Microsoft Defender for Cloud Apps or custom notifications via Logic Apps.

- **Integration with Conditional Access**  
  - Risk signals appear as “SignInRisk” condition.  
  - Conditional Access can require MFA if sign-in risk is medium/high.

**Smart Exam Tips**  
1. **License Requirement**  
   - Identity Protection requires Azure AD P2 for risk detection and remediation policies.  
   - Without P2, only “MFA Registration Policy” is available under P1.  
2. **Understanding Risk Levels**  
   - **Impossible travel**: Sign-ins from distant locations within unrealistic timespan.  
   - **Anonymous IP**: Sign-in from Tor nodes or VPN.  
   - **Leaked credentials**: Detected via Microsoft’s threat intelligence feeds.  
3. **Policy Ordering**  
   - When multiple risk policies apply, the strictest control wins (e.g., “Block access” supersedes “Require MFA”).  
   - Know how overlapping Conditional Access and Risk Policy settings behave.  
4. **Monitoring Risk Detections**  
   - Use “Risky users” and “Risky sign-ins” blades.  
   - When asked to troubleshoot why a user was blocked, check “Risk event ID” in the audit logs.  
5. **MFA and Risk Policy Interaction**  
   - When a user is medium-risk, even if they passed MFA recently, they may be forced to register additional authentication methods.  
   - Understand “Continuous access evaluation” impact on risk policy enforcement.  
6. **Automation with Logic Apps**  
   - Risk events can trigger Logic Apps via “When a risk event occurs” connector.  
   - Know basic Kusto Query Language (KQL) to query risk events in Azure Monitor if exam question demands log inspection.

---

## 5. Directory Synchronization Methods

**Summary**  
Synchronizing on-premises AD with Microsoft Entra ID ensures hybrid identity scenarios. Main methods:

- **Azure AD Connect (AAD Connect)**  
  - **Password Hash Synchronization (PHS)**: Hashes and syncs password hashes to the cloud; simplest setup.  
  - **Pass-Through Authentication (PTA)**: Authenticates directly against on-premises AD over a secure agent; no password hashes stored in cloud.  
  - **Federation (AD FS)**: Redirects authentication to on-premises AD FS; supports custom claim rules and advanced scenarios.

- **Seamless Single Sign-On (Seamless SSO)**  
  - Available with both PHS and PTA; automatically signs users in when on corporate network.

- **Azure AD Cloud Sync**  
  - Lightweight sync using a cloud-native sync agent; no SQL dependency.  
  - Supports syncing selected OUs and attribute filtering.

- **Federation Considerations**  
  - **AD FS**: Requires Windows Server 2016+ for modern authentication, high-availability deployment recommended.  
  - **Third-Party Federation** (Ping, Okta): Can integrate via SAML/OAuth; know trust-lane concepts.

**Smart Exam Tips**  
1. **PHS vs PTA vs Federation**  
   - **PHS**: Easiest—password hashes stored in Azure AD (no on-premises requirement for sign-in).  
   - **PTA**: Real-time authentication; requires 24/7 on-premises agent availability.  
   - **Federation**: Full control of authentication policies, but more infrastructure complexity (AD FS farm, Web Application Proxy).  
2. **Health Monitoring**  
   - Understand how to use “Azure AD Connect Health” to monitor sync errors, sign-in failures for PTA/AD FS.  
   - Know that “Azure AD Connect Health Agent for AD FS” requires installation on each AD FS server.  
3. **Staging vs Production Mode**  
   - AAD Connect supports staging mode for high-availability sync: only one staging server should be in “Staging mode.”  
   - Sync scheduler interval: 30 minutes by default; manual sync with `Start-ADSyncSyncCycle -PolicyType Initial/Delta`.  
4. **Cloud Sync Agent vs AAD Connect**  
   - Cloud Sync agent cannot write-back certain attributes (e.g., password writeback).  
   - Use Cloud Sync for multiple forests that aren’t network-connected; AAD Connect is preferred for password writeback.  
5. **Federation Token Lifetime**  
   - AD FS issues tokens with default 1-hour lifetime; demographic scenarios may require adjusting token lifetime (Set-ADFSProperties –TokenLifetime).  
   - Know how to troubleshoot SAML sign-in issues (“Trust relationship” errors).  
6. **Password Writeback Considerations**  
   - PHS with “Password writeback” enabled allows users to reset on-premises passwords via SSPR.  
   - Requires Azure AD P1/P2 and on-premises AD Connect without PTA.

---

## 6. Authentication Options (Password Hash Sync, Pass-Through, Federation, Passwordless)

**Summary**  
Selecting the appropriate authentication method balances security, complexity, and user experience. Details:

- **Password Hash Synchronization (PHS)**  
  - Simplest, requires minimal on-prem infrastructure.  
  - Cloud-only authentication after initial sync; risk if hash compromised.  
  - Supports Seamless SSO.

- **Pass-Through Authentication (PTA)**  
  - Credentials validated against on-premises AD in real time.  
  - Requires at least two on-premises authentication agents for high availability.  
  - No password hash stored in the cloud.

- **Federation (AD FS or Third-Party)**  
  - Full control of auth policy, supports custom claim rules (e.g., RADIUS, LDAP).  
  - Requires WAP (Web Application Proxy) servers for external access.  
  - Can enable smart card or certificate-based auth.

- **Passwordless Methods**  
  - **FIDO2 Security Keys**: Physical key (e.g., YubiKey) using WebAuthn. Requires modern browsers.  
  - **Microsoft Authenticator (Phone Sign-in)**: Approve push notifications or use phone PIN/biometrics.  
  - **Windows Hello for Business**: Certificate or key-based auth at device level with TPM.  
  - Configure under “Authentication Methods” in Entra ID; assign to groups via Conditional Access.

- **Legacy Protocols and Lockdown**  
  - Block Basic Authentication (POP, IMAP, SMTP) in Exchange Online to reduce exposure.  
  - Enforce OAuth2 (Modern Authentication) for Exchange, SharePoint, Skype for Business.

**Smart Exam Tips**  
1. **Agent Requirements for PTA**  
   - Each PTA agent must have outbound connectivity over port 443 to Azure; no inbound ports needed.  
   - If all agents go offline, users cannot authenticate unless fall back to PHS.  
2. **Pass-Through vs Federation Failover**  
   - Federation with AD FS has a fallback option only if AAD Connect is configured with PHS as backup.  
   - PTA fails closed: if the agent is unavailable, authentication is denied.  
3. **Deploying FIDO2**  
   - Must configure “Authentication methods policy” under Security > Authentication methods.  
   - Know how to enable “Allow users to register security info” and select groups gradually.  
4. **Windows Hello for Business Deployment**  
   - Requires hybrid Azure AD joined devices for certificate-based WHfB; key-based WHfB supports purely cloud environment.  
   - Understand how to configure Intune or Group Policy for WHfB provisioning.  
5. **Blocking Legacy Protocols**  
   - Use Exchange Online Conditional Access policies—create a policy targeting “Client apps” and exclude “Mobile apps and desktop clients”; block “Other clients (e.g., POP, IMAP).”  
   - Confirm blocking via “Sign-in logs” filter for “Client app: Other clients.”  
6. **Passwordless and Conditional Access**  
   - Create a Conditional Access policy requiring “Passwordless” as a strong authentication method for specified high-risk users (e.g., Global Administrators).  
   - Use grant control “Require authentication strength = Passwordless.”

---

## 7. Single Sign-On (SSO) and Identity Provider Integration

**Summary**  
Configuring SSO allows users to access multiple applications without repeated logins. Essentials include:

- **SSO Protocols**  
  - **SAML 2.0**: Common for enterprise apps (e.g., Salesforce, Workday).  
  - **WS-Fed (WS-Trust)**: Legacy Microsoft apps (e.g., SharePoint on-premises).  
  - **OAuth2 / OpenID Connect**: Modern web/mobile apps using tokens (e.g., custom web APIs).

- **Enterprise Application Configuration**  
  - Register an application in “App registrations” if building custom integration.  
  - For pre-integrated SaaS apps, use “Enterprise applications” gallery; follow the step-by-step wizard to configure SAML metadata, reply URL, and claims mapping.

- **Custom Claims and Attribute Mapping**  
  - Map Azure AD attributes (e.g., email, UPN, group claims) into the SAML token or ID token.  
  - Configure “Group claims” to send up to 200 group object IDs; use Azure AD groups in app roles.

- **Identity Provider (IdP) vs Service Provider (SP)**  
  - Microsoft Entra ID acts as IdP for SSO.  
  - Understand how to configure an external IdP (Okta, Ping) to authenticate into Azure AD–protected resources via federation.

- **Application Proxy (Connector-Based SSO)**  
  - Publish on-premises web apps behind the firewall using Azure AD Application Proxy.  
  - Use header-based pre-authentication or passthrough if the app uses Integrated Windows Auth.

**Smart Exam Tips**  
1. **SAML Parameter Matching**  
   - Make sure “Identifier (Entity ID)” and “Reply URL” (Assertion Consumer Service URL) match exactly between Azure AD and the application’s metadata.  
   - Common exam scenario: user cannot sign-in because the URL is missing a trailing slash.  
2. **Group Claims and Token Size**  
   - If a user is member of >150 groups, Azure AD sends a “hasgroups” claim in the token, forcing the app to call Microsoft Graph to retrieve full group list.  
   - Know how to troubleshoot “Token too large” errors by enabling group filtering or using “transitiveGroupMembership.”  
3. **App Roles vs Group Claims**  
   - Define `appRoles` in the application manifest for role-based authorization.  
   - Assign users/groups to these app roles under “Enterprise applications > Users and groups.”  
4. **OIDC vs OAuth2 Flows**  
   - Authorization Code Flow: Use for web server applications requiring access tokens and ID tokens.  
   - Implicit Flow (deprecated): Recognize that implicit flow is not recommended; Authorization Code with PKCE is preferred.  
5. **Application Proxy Pre-authentication**  
   - “Azure AD pre-authentication” means users authenticate with Azure AD before the proxy forwards traffic.  
   - “Passthrough” bypasses Azure AD, so securing the app must be done on-premises.  
6. **External IdP Federation**  
   - For federation with a third-party IdP, create a new “Identity provider” under “External Identities > All identity providers.”  
   - Configure the IdP’s metadata URL, client ID, client secret, and supported claims.

---

## 8. Modern Authentication Protocol Enforcement

**Summary**  
Legacy protocols (Basic Authentication, NTLM, Kerberos) lack MFA support and pose higher risk. Ensuring only modern protocols are used is critical:

- **Enforce TLS 1.2+**  
  - All services (Exchange Online, SharePoint Online) must use TLS 1.2 or later.  
  - Disable support for older protocols (TLS 1.0, TLS 1.1) in conditional access or service settings.

- **Block Basic Authentication**  
  - Use Conditional Access policies targeting “Client apps” → “Other clients (POP, IMAP, SMTP, MAPI)” and choose “Block.”  
  - For Exchange Online, review the “Authentication Policies” blade to create policies that block specific protocols.

- **Require OAuth2/Modern Authentication**  
  - Ensure apps use OAuth2 grant flows (e.g., authorization code with PKCE).  
  - Understand how to configure “Conditional Access: Require MFA” for Exchange Web Services, Outlook, and other legacy routes.

- **Legacy Protocol Reporting**  
  - Use the “Sign-in logs” filter for “Client app: Other clients” to identify legacy protocol usage.  
  - Configure “Azure AD authentication policy” to block legacy sign-ins at the tenant level (e.g., `Set-OrganizationConfig -OAuth2ClientProfileEnabled $true` in Exchange Online PowerShell).

**Smart Exam Tips**  
1. **Conditional Access for Blocking Legacy**  
   - Create a policy: Assign to “All users,” target “Office 365 Exchange Online,” and under “Client apps,” select “Other clients,” then “Block access.”  
   - Always place legacy-blocking policies in report-only mode first to avoid unintended lockouts.  
2. **Exchange Online Authentication Policies**  
   - Use Exchange Online PowerShell:  
     ```powershell
     New-AuthenticationPolicy -Name "Block Legacy Auth" -AllowBasicAuthPop $false -AllowBasicAuthImap $false -AllowBasicAuthSmtp $false -AllowBasicAuthActiveSync $false
     ```
   - Assign policy to mailboxes with `Set-User -Identity user@contoso.com -AuthenticationPolicy "Block Legacy Auth"`.  
3. **TLS Decommission Timeline**  
   - Be familiar with Microsoft deprecation announcements (e.g., “TLS 1.0/1.1 retirement for Azure in 2024”).  
   - Know how to verify protocol usage via network capture or Fiddler.  
4. **OAuth2 Enforcement on Hybrid Environments**  
   - For hybrid Exchange (on-premises + Exchange Online), ensure OAuth2 is enabled for cross-premises mail flow (hybrid modern authentication).  
   - Understand how to run `Set-OrganizationConfig -OAuth2ClientProfileEnabled $true`.  
5. **Monitoring Legacy Use**  
   - In Azure AD “Workbooks,” use the “Legacy Authentication Report” Workbook to track daily/weekly usage trends.  
   - When asked in the exam why legacy sign-in still occurs, check for “BasicAuthenticationRequestsNotAllowed” sign-in errors.  
6. **Service Principal Context**  
   - Some service principals (third-party app integrations) might still attempt legacy protocols.  
   - Know how to identify and disable those apps by reviewing “Enterprise applications” sign-in logs.

---

## 9. Azure Management Scope and RBAC Overview

**Summary**  
Controlling access to Azure resources requires understanding the hierarchy (management groups, subscriptions, resource groups, resources) and how RBAC roles apply. Key points:

- **Management Group Hierarchy**  
  - Parent of multiple subscriptions.  
  - Policies and RBAC assignments at management group level propagate to all child subscriptions.

- **Subscription and Resource Group Scope**  
  - **Subscription**: Billing boundary; assign roles (Owner, Contributor, Reader).  
  - **Resource Group**: Logical container; group related resources (VMs, storage accounts).  
  - **Resource**: Individual service (VM, Key Vault).

- **Built-in Roles**  
  - Owner (full access + assign RBAC), Contributor (manage resources, not access), Reader (view only).  
  - User Access Administrator (manage RBAC role assignments).  
  - Resource-specific built-in roles (e.g., “Virtual Machine Contributor,” “Storage Blob Data Reader”).

- **Custom Roles**  
  - Defined by JSON: `Actions`, `NotActions`, `DataActions`, `NotDataActions`, `AssignableScopes`.  
  - Use Azure CLI or PowerShell to create (`New-AzRoleDefinition`).  
  - Assign at appropriate scope to enforce least privilege.

- **Azure AD Roles vs Azure RBAC Roles**  
  - Azure AD roles manage directory objects (user, group, app registrations).  
  - Azure RBAC roles manage Azure resource operations (VM start/stop, storage read/write).

**Smart Exam Tips**  
1. **Scope Precedence**  
   - A deny assignment at any scope overrides permissions granted at parent scope.  
   - Know how to troubleshoot using “Access control (IAM) > View access” blade and “Effective permissions.”  
2. **Custom Role JSON Structure**  
   - Example snippet:
     ```json
     {
       "Name": "Storage Blob Data Uploader",
       "Actions": [
         "Microsoft.Storage/storageAccounts/blobServices/containers/write",
         "Microsoft.Storage/storageAccounts/listKeys/action"
       ],
       "AssignableScopes": [
         "/subscriptions/{subscription-id}/resourceGroups/{rg-name}"
       ]
     }
     ```
   - Understand `DataActions` vs `Actions` for data plane vs control plane.  
3. **Hierarchy and Propagation**  
   - Granting a role at management group level automatically extends to all subscriptions under it; verify inheritance.  
   - Remove an inherited assignment by applying a deny assignment on a child scope.  
4. **Azure AD vs Azure RBAC Example**  
   - To reset another user’s password in Azure AD, assign them the “Authentication Administrator” (Azure AD role).  
   - To stop a VM in Azure, assign them “Virtual Machine Contributor” (Azure RBAC).  
5. **Privilege Sensitivity**  
   - User Access Administrator can grant any role; use PIM to require JIT for User Access Administrator role.  
   - Always look for “Privileged role” in RBAC assignments.  
6. **RBAC Assignment Tools**  
   - Azure portal, Azure CLI (`az role assignment create`), PowerShell (`New-AzRoleAssignment`), ARM templates.  
   - Know syntax:  
     ```powershell
     New-AzRoleAssignment -ObjectId <object-id> -RoleDefinitionName "Reader" -Scope "/subscriptions/{sub-id}"
     ```

---

## 10. Privileged Identity Management (PIM)

**Summary**  
PIM enforces just-in-time (JIT) and approval workflows for Azure AD and Azure resource roles. Critical components:

- **PIM for Azure AD Roles**  
  - **Eligible vs Active Assignments**: Eligible users must “activate” a role; active users have permanent assigned privileges until expiration.  
  - **Approval Workflow**: Require one or more approvers (role owners) to approve activation.  
  - **Approval Notification**: Email notification with approval link; approval can be time-boxed.

- **PIM for Azure Resources**  
  - **JIT Access**: Users request elevation (e.g., “Owner” for a subscription) for specified duration (1–24 hours).  
  - **MFA Enforcement**: Activation requires MFA.  
  - **Activity Logs**: All activation, approval, and expiration events are logged under “Audit logs.”

- **Alerts and Justification**  
  - Configure PIM notifications for expiring roles, activation, and elevation.  
  - Require justifications during activation to capture purpose.

- **Review and Expiration**  
  - Set up “Access reviews” for PIM assignments; recurring reviews for eligible assignments.  
  - Configure “Auto-removal” if user fails to respond or if role no longer meets criteria.

**Smart Exam Tips**  
1. **License Requirement**  
   - Azure AD PIM requires Azure AD Premium P2.  
   - PIM for Azure resources is covered under Azure AD P2 licensing—no extra cost beyond that.  
2. **Eligible vs Active Lifecycle**  
   - Eligible assignment does not grant permissions until user goes to PIM portal and activates.  
   - Active assignments are similar to static assignments; ensure minimal use.  
3. **Approval Chains**  
   - When configuring approval, know difference between “One approver” vs “Multiple approvers (all must approve).”  
   - If an approver is also ineligible for the role, approval flow fails—assign approvers outside the eligible roster.  
4. **JIT Request Parameters**  
   - Maximum activation duration: 24 hours for Azure AD roles; for Azure resources, can set up to 72 hours if resource type allows.  
   - Activation requires specifying “Reason” (justification); know impact on audit logs.  
5. **PIM Access Reviews**  
   - Schedule reviews for eligible and active assignments separately.  
   - Use “Recurring” every 30/60 days; know how to configure fallback if reviewer does not respond (“Remove access if no response”).  
6. **PIM Notifications**  
   - Enable email notifications for “Role activation,” “Role eligible expiration,” and “Role assignment changes.”  
   - Use integrated “Alerting” to forward to Microsoft Sentinel for automated incident response.

---

## 11. Identity Governance (Lifecycle Workflows, Entitlement Management, Access Reviews)

**Summary**  
Identity Governance ensures that user access remains appropriate throughout the identity lifecycle:

- **Lifecycle Workflows**  
  - **Automated Provisioning/Deprovisioning** via HR systems (Workday, SuccessFactors) connected through Microsoft Graph API.  
  - Custom workflows using “Microsoft Entra ID Workflows” allow conditional steps (e.g., new hire needs manager approval for access).

- **Entitlement Management**  
  - **Access Packages**: Bundles of resources (Azure AD groups, SharePoint sites, applications).  
  - **Policies**: Define who can request, approval requirements (one-stage, multi-stage), expiration (30/60/90 days).  
  - **External Users**: Allow guest users to request access packages with their own approval chains.

- **Access Reviews**  
  - Periodic review of group memberships, app assignments, and privileged role assignments.  
  - Configure reviewers (user, manager, group owner); set recurrence.  
  - “Remediation” options: remove access if reviewer doesn’t respond, send reminders.

- **Entitlement Management Lifecycle**  
  - **Request**: User requests access package.  
  - **Approval**: Approvers review and approve/deny.  
  - **Assignment**: Package assignments provision groups/app roles.  
  - **Expiration/Recertification**: After expiration, access is revoked unless renewed via review.

**Smart Exam Tips**  
1. **Entitlement Management License**  
   - Requires Azure AD Premium P2.  
   - In exam scenarios, verify license level before selecting “Entitlement Management” solution.  
2. **Access Package Components**  
   - Know how to include combinations of: Azure AD groups, application roles, SharePoint Online sites, Teams.  
   - Understand how JIT can be configured (e.g., just request membership once, or every 90 days).  
3. **Access Review Setup**  
   - Create a review for “Guest users of Contoso Sales group” – set frequency to quarterly, reviewers as group owner.  
   - Know how to configure “Apply results” to remove users who are “Denied” or “Not reviewed.”  
4. **Workflow Designer Actions**  
   - Common actions: “Send email,” “Create Azure AD user,” “Update group membership,” “Invoke Microsoft Flow/Logic App.”  
   - Use conditions like “If department = HR” to branch logic.  
5. **Review Result Options**  
   - “Keep access” for those explicitly approved; “Remove access” for denied; “Take no action” for not reviewed if chosen.  
   - Understand “Fallback reviewers” if primary reviewer is unavailable.  
6. **Reporting and Compliance**  
   - Access Review summary appears in “Identity Governance” blade.  
   - For audit scenarios, export CSV of review decisions to provide evidence of compliance.

---

### Final Notes

- **Practice Hands-On**: Create a free Azure tenant and walk through each feature: MFA, Conditional Access, PIM, App Proxy, and entitlement workflows.  
- **Use Official Documentation**: Reference Microsoft Learn units and Tech Community blogs for detailed configuration steps.  
- **Master Terminology**: Differentiate between Azure AD roles vs Azure RBAC roles, PHS vs PTA vs Federation, SAML vs OAuth2 flows.  
- **Simulate Exam Scenarios**: When faced with a requirement (e.g., “block legacy protocols for Exchange Online”), articulate step-by-step how to implement in the portal or via PowerShell.  
- **Review Licensing Constraints**: Many advanced features (PIM, Identity Protection, Entitlement Management) require Azure AD Premium P2. Always check license before choosing a solution.

By reviewing each topic in this document and internalizing the **Smart Exam Tips**, you will be well-prepared to answer AZ-500 questions on Secure Identity and Access controls. Good luck.  
```1
