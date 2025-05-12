
[ Study guide for Exam AZ-500 ]

https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/az-500

[  ] 
https://learn.microsoft.com/en-us/credentials/certifications/azure-security-engineer/








AZ-500: Manage Security Controls for Identity and Access

This summary covers key concepts for managing security controls for identity and access, aligning with the AZ-500 exam objectives.

1. Role-Based Access Control (RBAC)
- Built-in Roles: Utilize predefined roles such as Owner, Contributor, and Reader to assign permissions to users, groups, and applications.
- Custom Roles: Create custom roles to tailor permissions to specific organizational needs.
- Role Assignments: Assign roles at different scopesâ€”subscription, resource group, or resource levelâ€”to control access granularity.

2. Microsoft Entra ID (formerly Azure Active Directory)
- User and Group Management: Manage identities, including creating and managing users and groups, and assigning roles.
- Privileged Identity Management (PIM): Implement PIM to manage, control, and monitor access within Microsoft Entra ID, ensuring just-in-time privileged access.
- Access Reviews: Conduct regular access reviews to ensure users have appropriate access levels, reducing the risk of excessive permissions.

3. Multi-Factor Authentication (MFA)
- MFA Implementation: Enforce MFA to add an extra layer of security, requiring users to provide additional verification methods.
- Conditional Access: Configure policies that require MFA based on specific conditions, such as user location or device compliance.

4. Conditional Access Policies
- Policy Configuration: Define policies that grant or block access based on conditions like user risk level, sign-in risk, or device state.
- Named Locations: Specify trusted IP ranges to control access from known locations.
- Session Controls: Implement session controls to limit user experience within applications, such as read-only access or blocking downloads.

5. Identity Protection
- Risk Detection: Utilize Microsoft Entra ID Protection to detect potential vulnerabilities affecting identities, such as leaked credentials or sign-ins from unfamiliar locations.
- Automated Responses: Configure automated responses to detected risks, like requiring password changes or blocking access.

6. Application Access Management
- App Registrations: Register applications within Microsoft Entra ID to manage authentication and authorization.
- Permission Management: Assign and manage API permissions for applications, ensuring they have appropriate access levels.
- Consent Framework: Utilize the consent framework to allow users or administrators to grant applications access to resources.

7. Managed Identities
- System-Assigned Managed Identity: Enable Azure services to authenticate to other services without storing credentials in code.
- User-Assigned Managed Identity: Create a standalone identity that can be assigned to multiple resources, providing greater flexibility.

8. Microsoft Entra Permissions Management
- Permissions Insights: Gain visibility into permissions across Azure, AWS, and GCP to identify unused or excessive permissions.
- Access Reviews: Conduct access reviews across multi-cloud environments to enforce least privilege access.

9. Monitoring and Reporting
- Audit Logs: Monitor activities within Microsoft Entra ID to track changes and access patterns.
- Sign-In Logs: Analyze sign-in logs to detect unusual activities or potential security incidents.
- Alerts and Notifications: Configure alerts to notify administrators of suspicious activities or policy violations.

10. Best Practices
- Least Privilege Principle: Always assign the minimum necessary permissions to users and applications.
- Regular Reviews: Periodically review access rights and adjust as necessary to maintain security.
- Secure Access: Combine Conditional Access and MFA to enhance security posture.
- Stay Informed: Keep up-to-date with Azure security features and best practices to adapt to evolving threats.

For a more in-depth understanding, consider exploring the following resources:
- Microsoft Learn: Manage Identity and Access - https://learn.microsoft.com/en-us/training/paths/manage-identity-access-new/
- AZ-500 Study Guide â€“ Section 1 - https://www.cloudpartner.fi/?p=17647
- Deep Dive into AZ-500: Managing Identity and Access - https://www.readynez.com/en/blog/deep-dive-into-az-500-managing-identity-and-access/