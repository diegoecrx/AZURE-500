# AZ-500 – Identity Management & Privileged Access (Microsoft Cloud Security Benchmark)

These notes condense the **Identity Management and Privileged Access** module into an exam-oriented study guide.

> **Scope** – IM-1 to IM-7 controls, with emphasis on Azure (Microsoft Entra ID) features that are frequently tested.  

## 1. Control Summaries

| ID  | Core Principle | Must-Know Azure Actions | Key Services/Tools |
|-----|----------------|-------------------------|--------------------|
| **IM-1**<br>Use a **centralized identity & authentication system** :contentReference[oaicite:0]{index=0} | Standardize on Microsoft Entra ID for all identities (cloud & on-prem). | • Create/secure a tenant<br>• Sync on-prem AD via AAD Connect<br>• Disable local auth on PaaS/IaaS | Entra ID, AD Connect |
| **IM-2**<br>**Protect** identity & auth systems :contentReference[oaicite:1]{index=1} | Treat Entra ID as Tier-0; restrict roles, enforce MFA, monitor risk. | • Review **Secure Score**<br>• Enable **Identity Protection** risk policies<br>• Deploy **Defender for Identity** | Secure Score, Identity Protection, Defender for Identity |
| **IM-3**<br>**Manage application identities** automatically :contentReference[oaicite:2]{index=2} | Replace human accounts with managed identities / service principals; automate rotation. | • Enable **System/User-assigned Managed Identity**<br>• Grant least-privilege RBAC<br>• Use cert-based creds | Managed Identities, Key Vault |
| **IM-4**<br>**Authenticate servers & services** (TLS) :contentReference[oaicite:3]{index=3} | Always use TLS 1.2+; validate server certs; support mutual TLS when required. | • Enforce minimum TLS via Policy<br>• Configure mutual TLS in API Management | TLS Policies, API Management |
| **IM-5**<br>**Single Sign-On (SSO)** for application access :contentReference[oaicite:4]{index=4} | Provide SSO with Entra ID to SaaS, PaaS & on-prem apps. | • Register enterprise apps<br>• Configure SAML/OIDC<br>• Set up SCIM provisioning | Entra ID Enterprise Apps |
| **IM-6**<br>Use **strong authentication controls** :contentReference[oaicite:5]{index=5} | Default to passwordless or MFA; prioritise privileged roles. | • Enable Azure MFA / FIDO2 / Windows Hello<br>• Block legacy auth<br>• Configure Password Protection | Azure MFA, Passwordless |
| **IM-7**<br>**Restrict access based on conditions** (Conditional Access) :contentReference[oaicite:6]{index=6} | Apply Zero-Trust signals (user, device, risk, location). | • Build CA policies (MFA, IP, device, session)<br>• Analyse CA Insights & Reporting | Conditional Access |

---

## 2. Quick-Fire Revision Checklist

- **Tenant security** – custom domains, global admin redundancy, no legacy auth.  
- **Risk remediation** – user & sign-in risk policies, Secure Score recommendations.  
- **Managed identities** – enable, assign RBAC, rotate secrets automatically.  
- **TLS everywhere** – enforce via Azure Policy; verify cert chains in clients.  
- **SSO flows** – SAML, OIDC, OAuth 2.0; provisioning via SCIM.  
- **Passwordless & MFA** – choose correct method; configure registration policies.  
- **Conditional Access** – plan, implement, and troubleshoot layered policies.

---

## 3. Practice Tasks for the Exam Lab

1. **Configure** an Entra ID tenant, add a custom domain, and sync on-prem AD.  
2. **Enable** Identity Protection, review a risky sign-in, and remediate.  
3. **Assign** a system-assigned managed identity to a VM and grant it Key Vault Reader.  
4. **Enforce** minimum TLS 1.2 on a Storage Account with Azure Policy.  
5. **Integrate** a SaaS app with SAML SSO and test user provisioning.  
6. **Deploy** Azure MFA with Conditional Access requiring MFA for privileged roles.  
7. **Create** a Conditional Access policy blocking legacy authentication.

---

## 4. Exam Tips

- Memorise where each Entra feature lives in the portal and its CLI/PowerShell equivalents.  
- Understand licensing requirements (e.g., P1 vs P2 for Identity Protection & CA).  
- Expect scenario questions combining CA, MFA, and role assignments—know precedence rules.  

---

**Total module time:** ≈ 15 min — invest extra lab time to internalise each control.
