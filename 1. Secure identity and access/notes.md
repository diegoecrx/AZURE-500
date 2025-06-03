

### Manage security controls for identity and access ###




** Identity management and privileged access






# Microsoft Cloud Security Benchmark: Identity Management & Privileged Access

---

## IM-1: Use Centralized Identity and Authentication System

**Objective:**  
Use a single identity system to manage user authentication and access across cloud and on-premises resources.

**Key Actions:**

- Centralize identity using Microsoft Entra ID for users, applications, and services.
- Minimize the use of local accounts or separate identity systems.
- Synchronize on-premises identities via Microsoft Entra Connect or Microsoft Entra Cloud Sync.
- Integrate third-party identity providers if necessary, using federation.

**Microsoft Tools and Resources:**

- [Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-whatis)
- [Azure AD Connect](https://learn.microsoft.com/en-us/azure/active-directory/hybrid/whatis-azure-ad-connect)
- [External Identity Providers](https://learn.microsoft.com/en-us/azure/active-directory/b2b/direct-federation)

---

## IM-2: Use Strong Authentication Controls

**Objective:**  
Protect user accounts and access with robust authentication mechanisms.

**Key Actions:**

- Require Multi-Factor Authentication (MFA) for all users, especially privileged accounts.
- Implement passwordless authentication options (e.g., Windows Hello, FIDO2, Microsoft Authenticator).
- Use Conditional Access policies to enforce MFA under specific conditions (e.g., location, risk level, device compliance).

**Microsoft Tools and Resources:**

- [MFA Deployment](https://learn.microsoft.com/en-us/azure/active-directory/authentication/tutorial-enable-azure-mfa)
- [Passwordless Sign-in](https://learn.microsoft.com/en-us/azure/active-directory/authentication/concept-authentication-passwordless)

---

## IM-3: Manage Identity Lifecycle

**Objective:**  
Ensure proper handling of identity creation, modification, and deletion.

**Key Actions:**

- Automate user provisioning and deprovisioning using Microsoft Entra ID features.
- Define processes for employee onboarding, role changes, and offboarding.
- Review and update user access regularly through Access Reviews.
- Manage identities for external users appropriately using Microsoft Entra B2B.

**Microsoft Tools and Resources:**

- [Lifecycle Workflows](https://learn.microsoft.com/en-us/azure/active-directory/governance/workflows-overview)
- [Access Reviews](https://learn.microsoft.com/en-us/azure/active-directory/governance/access-reviews-overview)
- [Cloud Sync](https://learn.microsoft.com/en-us/azure/active-directory/cloud-sync/what-is-cloud-sync)

---

## IM-4: Use Role-Based Access Control (RBAC)

**Objective:**  
Assign permissions based on user roles to reduce risk and maintain control.

**Key Actions:**

- Use Azure built-in roles for common tasks.
- Define custom roles for specialized scenarios.
- Apply the principle of least privilege.
- Use groups to assign roles where possible for simplified management.

**Microsoft Tools and Resources:**

- [RBAC Overview](https://learn.microsoft.com/en-us/azure/role-based-access-control/overview)
- [Create Custom Roles](https://learn.microsoft.com/en-us/azure/role-based-access-control/custom-roles)

---

## IM-5: Monitor and Audit Identity Activities

**Objective:**  
Detect suspicious behavior and maintain accountability through logs and analytics.

**Key Actions:**

- Collect and analyze sign-in and audit logs.
- Enable Microsoft Entra ID Protection to detect risky sign-ins and users.
- Set up alert rules for critical identity-related events.
- Integrate with SIEM tools like Microsoft Sentinel for deeper correlation and investigation.

**Microsoft Tools and Resources:**

- [Sign-in Logs](https://learn.microsoft.com/en-us/azure/active-directory/reports-monitoring/concept-sign-ins)
- [Identity Protection](https://learn.microsoft.com/en-us/azure/active-directory/identity-protection/overview-identity-protection)
- [Audit Logs](https://learn.microsoft.com/en-us/azure/active-directory/reports-monitoring/concept-audit-logs)

---

## IM-6: Secure Privileged Access

**Objective:**  
Protect accounts with elevated permissions from compromise and misuse.

**Key Actions:**

- Implement Microsoft Entra Privileged Identity Management (PIM).
- Enforce just-in-time (JIT) access and time-bound role activations.
- Require approval workflows and MFA for role activation.
- Review role assignments and privileged role usage regularly.

**Microsoft Tools and Resources:**

- [Privileged Identity Management](https://learn.microsoft.com/en-us/azure/active-directory/privileged-identity-management/pim-configure)
- [PIM Just-In-Time Access](https://learn.microsoft.com/en-us/azure/active-directory/privileged-identity-management/pim-how-to-activate-role)
- [Privileged Access Strategy](https://learn.microsoft.com/en-us/security/benchmark/azure/security-controls-v3-identity-management#im-6-secure-privileged-access)

---

## Summary for Exam Preparation

- Memorize what each IM- control is responsible for and how Microsoft tools implement them.
- Understand best practices like least privilege, MFA, lifecycle management, and JIT access.
- Focus on key services: Microsoft Entra ID, PIM, Conditional Access, RBAC, and logging tools.
- Know how to configure, monitor, and audit privileged and regular user accounts.

















### Manage Microsoft Entra application access ###
