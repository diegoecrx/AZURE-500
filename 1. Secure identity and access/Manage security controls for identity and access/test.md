# AZ-500: Secure Identity and Access – Consolidated Study Guide

This document covers each module in the “Secure Identity and Access” learning path. For each module, key concepts are outlined along with focused tips to help you prepare for the AZ-500 exam.

---

## Module 1: Manage Security Controls for Identity and Access

### Overview
This module teaches how to secure identities, authentication, and authorization in Microsoft Entra ID. It covers:
- Securing Microsoft Entra users and groups
- Managing external identities
- Implementing Microsoft Entra Identity Protection
- Configuring synchronization (Azure AD Connect, Cloud Sync)
- Choosing and deploying authentication methods (password hash sync, pass-through authentication, federation)
- Enforcing multifactor authentication (MFA) and passwordless options
- Implementing Conditional Access policies
- Configuring single sign-on (SSO) and identity providers
- Applying modern authentication protocols
- Securing management scope with management groups and RBAC at subscription/resource level
- Defining Zero Trust concepts and integrating Privileged Identity Management (PIM)
- Configuring identity governance (lifecycle management, access reviews, entitlement management)

#### 1. Secure Microsoft Entra Users
- **Create and manage user accounts.**  
  - Understand manual vs bulk provisioning.  
  - Know how to assign and reset passwords, delegate user account management.
- **Password protection**  
  - Configure banned password lists, smart lockout.
- **Implement MFA**  
  - Enforce MFA registration.  
  - Use Conditional Access to require MFA based on risk or location.

#### 2. Secure Microsoft Entra Groups
- **Group types**  
  - Security groups vs Microsoft 365 groups.  
  - Use dynamic group membership to automate assignment.
- **Group-based licensing**  
  - Assign licenses at group level to simplify user management.
- **Privileged groups**  
  - Harden access to groups that grant elevated privileges (e.g., Global Administrator membership).

#### 3. External Identities
- **When to use external identities**  
  - B2B collaboration vs B2C  
  - Guest access for contractors or partners.
- **Secure external identities**  
  - Enforce MFA or Conditional Access for guest users.  
  - Limit guest user permissions (restrict directory browsing, restrict access to certain resources).

#### 4. Microsoft Entra Identity Protection
- **Risk events and detections**  
  - Detect leaked credentials, atypical travel, risky IP, and other risk indicators.
- **User and sign-in risk policies**  
  - Configure policies to block or require MFA based on risk level.
- **Remediation workflow**  
  - Automate remediation (password reset, block user) based on risk detections.

#### 5. Directory Synchronization
- **Azure AD Connect**  
  - Understand federation vs password hash synchronization vs pass-through authentication.  
  - Know when to use Seamless SSO.
- **Microsoft Entra Cloud Sync**  
  - Use Cloud Sync agent for lightweight synchronization scenarios.
- **Federation with on-premises AD FS**  
  - Configure and troubleshoot federation.  
  - Understand how federation differs from pass-through authentication.

#### 6. Authentication Options
- **Password hash sync (PHS)**  
  - Simplest, lowest-maintenance option.  
  - Understand risk of password hash compromise.
- **Pass-through authentication (PTA)**  
  - Authenticate directly against on-premises AD.  
  - Know performance and availability considerations.
- **Federation (AD FS)**  
  - Full control over authentication policies.  
  - Knowledge of certificate requirements, token lifetimes.
- **Kerberos and NTLM**  
  - Understand legacy authentication protocols and their limitations.
- **Passwordless methods**  
  - FIDO2 security keys, Microsoft Authenticator app, Windows Hello for Business.  
  - Configure and enforce passwordless for specific user groups.
- **Password protection**  
  - Configure lockout and banned password lists.

#### 7. Single Sign-On (SSO) and Identity Providers
- **SSO concepts**  
  - Integrated Windows authentication vs SAML vs OAuth 2.0 / OpenID Connect.
- **Configure SSO**  
  - Set up SAML-based SSO for enterprise applications.  
  - Create app registrations for OpenID Connect/OAuth2 clients.
- **Identity provider integration**  
  - Add external identity providers (Google, Facebook) for B2C scenarios.

#### 8. Modern Authentication Protocols
- **Enforce TLS 1.2+**
- **Disable legacy protocols** 
  - Block Basic Authentication, ensure services use modern OAuth flows.

#### 9. Azure Management Scope and RBAC
- **Management groups**  
  - Organize subscriptions into hierarchies.  
  - Assign policies or RBAC at management group level for uniform governance.
- **RBAC fundamentals**  
  - Built-in roles (Owner, Contributor, Reader, User Access Administrator).  
  - Custom roles: define using JSON, assign to specific scopes.
- **Azure built-in roles vs Microsoft Entra roles**  
  - Understand scope differences: Azure RBAC controls resource actions; Microsoft Entra roles control directory actions.

#### 10. Privileged Identity Management (PIM)
- **Purpose**  
  - Enforce Just-In-Time (JIT) access to privileged roles.  
  - Require approval and MFA to activate roles.
- **Configure PIM**  
  - Assign eligible vs active assignments.  
  - Set up approval workflows, specify approval owners.
- **PIM for Azure Resources vs Entra roles**  
  - Understand differences in scope and licensing (P2 requirement).

#### 11. Identity Governance
- **Identity lifecycle management**  
  - Automate user provisioning/deprovisioning with provisioning workflows or SCIM.
- **Lifecycle workflows**  
  - Use Microsoft Entra ID Workflows to automate HR-driven provisioning.
- **Entitlement management**  
  - Create access packages for internal or external users.  
  - Define policies: expiration, approval, multi-stage approval.
- **Access reviews**  
  - Schedule periodic reviews for groups, app assignments, privileged roles.  
  - Configure reviewers and recurrence.  
  - Automate removal if no response.

---

### Exam Tips for Module 1

- **Know synchronization scenarios**   
  - Be prepared to choose between PHS, PTA, and federation based on requirements (high availability, password writeback, seamless SSO).  
  - Understand how Pass-through Authentication proxies and Azure AD Connect health agent function.

- **Practice Conditional Access policies**   
  - Be able to configure policies targeting user risk, sign-in risk, location (named locations), and device compliance.   
  - Know how to simulate policies (report-only mode) before enforcement.

- **Memorize key PIM concepts**   
  - Know how to assign eligible roles, configure notification settings, and set up approval workflows.   
  - Understand difference between PIM for Azure resources and PIM for Entra roles.

- **Understand authentication protocol choices**   
  - If an organization cannot synchronize password hashes, you must choose federation with AD FS or PTA.  
  - Know trade-offs: PHS provides fastest sign-in; PTA depends on on-prem connectivity; federation allows custom claim rules.

- **Identity Protection and risk remediation**   
  - Know the built-in risk detections (Leaked credentials, Atypical travel, Malware linked IP).  
  - Practice configuring user risk and sign-in risk policies to block or require password change/MFA.  
  - Understand licensing requirements: Identity Protection requires P2.

- **RBAC and scope hierarchy**   
  - Clearly distinguish between management groups, subscriptions, resource groups, and resources.  
  - Know which built-in roles apply at each scope and when you need to create custom roles.

- **Access reviews and entitlement management**   
  - Be ready to configure a recurring access review for a group or application.   
  - Know how to create an access package that enforces policy-based governance (e.g., requiring group owner approval, expiration notifications).

- **SSO and app registrations**   
  - Be able to register an enterprise application for SAML-based SSO and assign users/groups.  
  - Know how to configure a native (mobile/Desktop) or web application using OAuth2/OpenID Connect.

- **Passwordless deployment**   
  - Understand how to roll out FIDO2 security keys or Microsoft Authenticator.   
  - Know enrollment steps and how to configure “Passwordless Security” in Entra ID.

---

## Module 2: Manage Microsoft Entra Application Access

### Overview
This module covers how to secure and manage access for applications that rely on Microsoft Entra ID for authentication and authorization. It includes:
- Controlling enterprise application access
- Managing app registrations and service principals
- Assigning API permissions and consenting to permissions
- Configuring Microsoft Entra Application Proxy for secure remote access to on-premises applications

#### 1. Enterprise Application Management
- **Enterprise applications vs App registrations**  
  - Enterprise Applications are service principals (instances of app registrations) used within your tenant.  
  - App registrations define identity configurations for your application (application ID, redirect URIs, certificates/secrets).
- **User and group assignment**  
  - Assign users/groups to enterprise apps – understand “Assign users and groups” vs “Users assignable to the app.”  
  - Use application roles (appRole) in the manifest to define custom roles within an enterprise app.

#### 2. Service Principals and Managed Identities
- **Service principals**  
  - Represent application identity in a tenant; used for authentication and permission grants.  
  - Know difference between Delegated Permissions (on-behalf-of user) vs Application Permissions (app identity without user).
- **Managed identities for Azure resources**  
  - System-assigned vs User-assigned.  
  - Azure creates a service principal automatically for system-assigned managed identity.  
  - Use managed identities to access Azure resources without storing credentials.

#### 3. App Registration and Permission Grants
- **App registration process**  
  - Register web/API or native/client app.  
  - Configure redirect URIs, certificates/secrets, and supported account types (Single-tenant vs Multi-tenant vs Personal Microsoft Accounts).
- **API permissions**  
  - Request Microsoft Graph or other API scopes.  
  - Admin consent vs user consent – understand least privilege and just-in-time consent.
- **Certificates and client secrets**  
  - Best practices: use certificates where possible, rotate secrets regularly, store secrets in Azure Key Vault.
- **Token configuration**  
  - Customize ID token and access token claims in the app registration.  
  - Add group claims for applications that need group membership information.

#### 4. Microsoft Entra Application Proxy
- **Deployment architecture**  
  - Azure AD Application Proxy connector installed on on-premises server.  
  - Connector establishes outbound connection to Azure; no inbound firewall rules required.
- **Publish on-premises applications**  
  - Configure internal URL and external URL.  
  - Assign pre-authentication method (Azure AD vs Passthrough).  
  - Understand header-based pre-authentication vs header preservation.
- **Secure remote access**  
  - Enforce Conditional Access for Application Proxy apps.  
  - Use Hybrid Connections if additional customization is required.
- **Connector groups**  
  - Assign multiple connectors to a group for high availability and load balancing.

#### 5. Monitoring and Troubleshooting
- **Sign-in and audit logs for enterprise apps**  
  - Analyze sign-in failures, protocol usage (SAML, WS-Fed, OAuth2).  
  - Audit changes to application configuration (who granted consent, configuration changes).
- **Conditional Access integration**  
  - Apply policies to enterprise applications published via App Proxy.
- **Service Principal health**  
  - Monitor federation endpoints, certificate expiration, service principal status.

---

### Exam Tips for Module 2

- **Differentiate between App Registration and Enterprise Application**  
  - In exam scenarios, you may be asked why users cannot sign in to an enterprise app – know you must assign users or groups to that enterprise application.
- **Service Principal vs Managed Identity**  
  - When securing access to Azure resources from code, prefer managed identities – understand both system-assigned and user-assigned flows.
- **API Permission Consent**  
  - If an application requests an API permission that requires admin consent (e.g., Directory.Read.All), use the “Grant admin consent” flow and know the Azure portal steps.
- **Application Proxy Pre-authentication**  
  - Know how to configure "Azure AD pre-authentication" to require users to authenticate with Entra ID before accessing internal apps.
- **Application Role Assignments**  
  - Practice adding `appRole` entries to the application manifest and assigning users to these roles so they appear in the user’s token claims.
- **OAuth2 Implicit vs Authorization Code Flow**  
  - Be clear on which flow to use for single-page applications vs web server scenarios.  
  - Understand how to configure “Supported account types” in the registration based on multi-tenant or single-tenant needs.
- **Connector Groups for High Availability**  
  - If an exam question describes high availability for on-premises apps, answer: deploy multiple connectors in a connector group.
- **Troubleshoot SSO Issues**  
  - When users cannot access an application, verify sign-in logs for “invalid_target” or “invalid_resource.”  
  - Check SAML configuration: reply URLs must match exactly; certificate revision if token signature fails.
- **Least-Privilege Permissions**  
  - When asked to give an application only read access to user profiles, choose “User.Read.All (Delegated)” rather than broader scopes like “Directory.Read.All”.
- **Token Lifetime and Signing Certificates**  
  - Know how to rotate a signing certificate without downtime (upload new certificate, switch priority, remove old certificate after tokens expire).

---

## General Exam Preparation Tips for Secure Identity and Access

1. **Hands-On Practice**  
   - Create a trial Azure tenant and practice configuring Entra ID features: MFA, Conditional Access, PIM, App Proxy.  
   - Use the Azure portal, PowerShell (`AzureAD` and `Az` modules), and Microsoft Graph Explorer to validate configurations.

2. **Understand Licensing Requirements**  
   - Identify which features require P1 vs P2 licenses (e.g., Identity Protection and PIM require P2, Access Reviews require P2).  
   - In exam scenarios, confirm the correct license tier before selecting an answer.

3. **Distinguish Between Similar Concepts**  
   - Pass-Through Authentication vs Federation vs Password Hash Sync  
   - Azure RBAC vs Microsoft Entra (Azure AD) roles  
   - Service Principal vs Managed Identity  
   - SAML vs OAuth2/OpenID Connect vs WS-Fed

4. **Memorize Default Conditional Access Controls**  
   - Know built-in named locations (Trusted IPs), device platform filters, and how to target “All cloud apps” vs specific apps.

5. **Focus on Zero Trust Principles**  
   - Understand how identity is the new perimeter.  
   - Be prepared to explain how Conditional Access fulfills Zero Trust requirements (Verify explicitly, Least privilege access, Assume breach).

6. **Review JSON for Custom Roles and Policies**  
   - Practice creating a custom role JSON with `Actions`, `NotActions`, `DataActions`, and assign it to a resource group.  
   - Know how to scope PIM assignment via resource, resource group, or subscription.

7. **Log Analysis and Reporting**  
   - Use Entra ID sign-in and audit logs, Azure Monitor, and Azure Sentinel; be familiar with Kusto Query Language (KQL) basics if Azure Sentinel is mentioned.

8. **Use Microsoft Learn Knowledge Checks**  
   - Complete the built-in quizzes in each unit to reinforce details.  
   - Take notes on nuanced differences (for example, how long a Conditional Access grant control (Require MFA) remains in the claim).

9. **Time Management**  
   - During the exam, allocate time for reading scenario-based questions carefully.  
   - Watch for keywords: “least privilege,” “temporary access,” “self-service,” “zero trust,” “external identities.”

10. **Stay Updated**  
   - Confirm any recent changes or new features in Entra ID (service name updates: Azure AD is now “Microsoft Entra ID”).  
   - Follow the official Azure updates page for announcements that might appear in exam questions (e.g., new passwordless features or updated MFA methods).

---

By mastering the content of these two modules and focusing on the exam tips provided, you will be well-prepared to tackle the AZ-500 questions related to Secure Identity and Access. Good luck with your preparation.0
