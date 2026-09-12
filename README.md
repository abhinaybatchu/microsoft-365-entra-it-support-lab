# Microsoft 365, Entra ID & Hybrid Identity IT Support Lab

## Overview

This project simulates Microsoft 365 and identity administration for a fictional organization named **Abhinay Labs**.

The lab was designed to build practical skills for entry-level **IT Support, Service Desk, Microsoft 365 Support, IAM, and IT Security Support** roles.

The project began with cloud-native Microsoft 365 and Microsoft Entra ID administration and later expanded into Microsoft 365 workload administration, authentication troubleshooting, least-privilege RBAC, Conditional Access, Microsoft Entra device identity, Microsoft Graph PowerShell, and controlled hybrid identity synchronization with an existing on-premises Active Directory environment.

All employee identities, company information, systems, and business data used in this project are synthetic and were created solely for the lab.

---

## Project Objectives

The project was designed to develop hands-on experience with:

- Microsoft 365 tenant administration
- Microsoft Entra ID user and group administration
- Microsoft 365 licensing and service provisioning
- Password and authentication support
- Sign-in and audit log investigation
- Microsoft Exchange Online administration
- Microsoft Teams administration
- SharePoint and OneDrive support
- Group-based access control
- Microsoft Entra administrative roles
- Least-privilege Help Desk administration
- Conditional Access evaluation
- Microsoft Entra device identity
- Microsoft Graph PowerShell
- Microsoft 365 Service Health investigation
- Microsoft Entra Connect Sync
- Password Hash Synchronization
- Hybrid identity source-of-authority concepts
- Identity synchronization troubleshooting
- Joiner, Mover, and Leaver support workflows
- Enterprise Help Desk troubleshooting methodology

---

## Lab Architecture

The project combines an existing on-premises Active Directory environment with a Microsoft 365 / Microsoft Entra cloud tenant.

```text
                          ABHINAY LABS
                 HYBRID IDENTITY LAB ENVIRONMENT


 ON-PREMISES ENVIRONMENT                          MICROSOFT CLOUD
 abhinaylabs.internal                             abhinaylabs.onmicrosoft.com

 â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                    â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
 â”‚        DC01 / DC02        â”‚                    â”‚     Microsoft Entra ID       â”‚
 â”‚                           â”‚                    â”‚                              â”‚
 â”‚ Active Directory DS       â”‚                    â”‚ Users                        â”‚
 â”‚ DNS                       â”‚                    â”‚ Cloud Security Groups        â”‚
 â”‚ Users / OUs / Groups      â”‚                    â”‚ Administrative Roles         â”‚
 â”‚ Domain Authentication     â”‚                    â”‚ Authentication / MFA         â”‚
 â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                    â”‚ Conditional Access           â”‚
               â”‚                                  â”‚ Sign-In Logs                 â”‚
               â”‚                                  â”‚ Audit Logs                   â”‚
               â”‚                                  â”‚ Device Identities            â”‚
               â”‚                                  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
               â”‚                                                 â”‚
               â”‚                                                 â”‚
     â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â–¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                         â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â–¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
     â”‚  Entra-Sync-Pilot  â”‚                         â”‚ Microsoft 365 Services   â”‚
     â”‚                    â”‚                         â”‚                          â”‚
     â”‚ David Miller       â”‚                         â”‚ Exchange Online          â”‚
     â”‚ Elena Rivera       â”‚                         â”‚ Microsoft Teams          â”‚
     â”‚ Joseph Daniel      â”‚                         â”‚ SharePoint Online        â”‚
     â”‚ Pauline Hudson     â”‚                         â”‚ OneDrive                 â”‚
     â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                         â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
               â”‚
               â”‚ Controlled user synchronization
               â–¼
     â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
     â”‚       SYNC01       â”‚
     â”‚                    â”‚
     â”‚ Microsoft Entra    â”‚
     â”‚ Connect Sync       â”‚
     â”‚                    â”‚
     â”‚ Password Hash      â”‚
     â”‚ Synchronization    â”‚
     â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
               â”‚
               â”‚ Existing-user matching
               â”‚ + synchronized attributes
               â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â–º
                                         Microsoft Entra ID


 ON-PREMISES ENDPOINT                              CLOUD-FIRST ENDPOINT

 â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                    â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
 â”‚         CLIENT01          â”‚                    â”‚       CLOUDCLIENT01       â”‚
 â”‚                           â”‚                    â”‚                           â”‚
 â”‚ Windows 11                â”‚                    â”‚ Windows 11 Enterprise     â”‚
 â”‚ AD domain joined          â”‚                    â”‚ Microsoft Entra joined    â”‚
 â”‚ abhinaylabs.internal      â”‚                    â”‚ DomainJoined : NO         â”‚
 â”‚                           â”‚                    â”‚ AzureAdJoined : YES       â”‚
 â”‚ Not hybrid Entra joined   â”‚                    â”‚ MDM / Intune : None      â”‚
 â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                    â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜


 ADMINISTRATION / SUPPORT

 â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
 â”‚ Microsoft 365 Admin Center | Entra Admin Center | Exchange Admin Center â”‚
 â”‚ Teams Admin Center | SharePoint | Microsoft Graph PowerShell            â”‚
 â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
````
**Hybrid Synchronization Scope**

The hybrid deployment intentionally used a **controlled pilot scope**.

Only these four synthetic employees were synchronized from on-premises AD DS to Microsoft Entra ID:

* David Miller
* Elena Rivera
* Joseph Daniel
* Pauline Hudson

The lab intentionally did **not** synchronize:

* The entire Active Directory directory
* On-premises Active Directory groups
* CLIENT01
* Other on-premises computer objects

The departmental Microsoft Entra security groups remained **cloud-managed groups**.

CLIENT01 remained a traditional Active Directory domain-joined workstation, while CLOUDCLIENT01 was deployed separately to demonstrate a Microsoft Entra joined, cloud-first Windows device.

This design allowed the project to demonstrate both traditional on-premises identity and modern cloud identity without unnecessarily expanding the synchronization scope.

---

## Technologies Used

| Technology                       | Purpose                                               |
| -------------------------------- | ----------------------------------------------------- |
| Microsoft 365 Business Premium   | Microsoft 365 services and cloud administration       |
| Microsoft Entra ID               | Cloud identity and access management                  |
| Microsoft Entra ID P1            | Conditional Access and identity features              |
| Exchange Online                  | Cloud mailbox administration                          |
| Microsoft Teams                  | Collaboration and policy administration               |
| SharePoint Online                | Team content and resource permissions                 |
| OneDrive                         | Individual business file storage and administration   |
| Microsoft Graph PowerShell       | Repeatable Microsoft 365 / Entra administration       |
| Microsoft Entra Connect Sync     | On-premises AD DS to Entra identity synchronization   |
| Active Directory Domain Services | Existing on-premises identity source                  |
| Windows Server                   | Domain controllers and synchronization infrastructure |
| Windows 11 Enterprise            | Microsoft Entra joined client testing                 |
| PowerShell                       | Administration, validation, and troubleshooting       |

---

# Major Implementation Areas

## 1. Microsoft Entra ID User Administration

Created and administered synthetic organizational identities for:

* Human Resources
* Finance
* Sales
* Information Technology

Configured organizational attributes including department, job title, company, employee type, and usage location.

Practiced account enable/disable operations, administrative password reset, and user-state validation.

![Microsoft Entra Users](02-screenshots/02-entra-cloud-users.png)

---

## 2. Groups and Access Management

Created assigned Microsoft Entra security groups representing departmental and job-function access.

Examples included:

* `SG-HR-Users`
* `SG-Finance-Users`
* `SG-Sales-Users`
* `SG-IT-Users`
* `SG-IT-Helpdesk`

The lab emphasized group-based access rather than unnecessary direct user permissions.

![Microsoft Entra Security Groups](02-screenshots/03-entra-security-groups.png)

---

## 3. Microsoft 365 Licensing and Service Provisioning

Assigned Microsoft 365 Business Premium licensing and validated the complete service-provisioning lifecycle.

This included verifying:

```text
Identity
   â†“
License
   â†“
Service Plan
   â†“
Service Provisioning
   â†“
End-User Access
```

Exchange Online mailbox provisioning was verified from the Exchange Admin Center.

![Microsoft 365 License Assignment](02-screenshots/05-m365-license-assignment.png)

![Exchange Online Mailbox](02-screenshots/06-exchange-mailbox-provisioning.png)

---

## 4. Authentication and Sign-In Troubleshooting

Simulated and investigated user authentication issues using Microsoft Entra sign-in logs.

A user-facing sign-in issue was correlated with Entra telemetry showing failed, interrupted, and successful authentication attempts.

Error code `50057` was investigated and identified as an account-disabled condition.

![Microsoft Entra Sign-In Log Investigation](02-screenshots/09-entra-signin-log-troubleshooting.png)

The lab reinforced an important troubleshooting principle:

> A user-facing error is a symptom. Administrative logs should be used to determine the recorded cause before applying remediation.

---

## 5. Licensing Troubleshooting

Demonstrated that successful authentication does not automatically provide access to Microsoft 365 services.

An unlicensed user successfully authenticated to Microsoft 365 but Outlook failed with:

```text
OwaUserHasNoMailboxAndNoLicenseAssignedException
```

The issue demonstrated the difference between:

```text
Identity
Authentication
License entitlement
Service provisioning
Application access
```

![Unlicensed Outlook User](02-screenshots/10-unlicensed-user-outlook-error.png)

---

## 6. SharePoint Authorization Troubleshooting

Configured group-based access to a Finance SharePoint resource.

A controlled authorization failure was generated by removing the Finance user from the appropriate security group.

The user remained authenticated but received:

```text
You need access
```

This demonstrated the difference between authentication and authorization.

![SharePoint Access Denied](02-screenshots/11-sharepoint-access-denied.png)

Access was restored through the approved group-based permission path rather than by creating unnecessary direct permissions.

---

## 7. Least-Privilege Help Desk Administration

Assigned the built-in **Helpdesk Administrator** Microsoft Entra role to the synthetic IT Support user Pauline Hudson.

The account was allowed to perform appropriate Help Desk operations while remaining restricted from higher-privilege role administration.

![Helpdesk Administrator Role](02-screenshots/12-entra-helpdesk-administrator-role.png)

This demonstrated:

* Role-Based Access Control
* Least privilege
* Separation of duties
* Delegated administration

---

## 8. Teams, SharePoint, and OneDrive Administration

Created and administered a private Finance Team and configured membership, ownership, channels, and a custom Teams messaging policy.

The policy was validated from the end-user perspective before returning the user to the appropriate production-style policy state.

![Teams Messaging Policy](02-screenshots/13-teams-messaging-policy-assignment.png)

The project also demonstrated that files stored in standard Teams channels are backed by SharePoint document libraries.

![Teams and SharePoint Integration](02-screenshots/14-teams-sharepoint-file-integration.png)

Authorized OneDrive administrative access was also tested for a simulated business-continuity scenario without using the employee's password.

![OneDrive Administrative Access](02-screenshots/15-onedrive-administrative-file-access.png)

---

## 9. Conditional Access

Created a Conditional Access policy for Elena Rivera in the Finance scenario, targeting Office 365 Exchange Online and requiring MFA, while keeping the policy in **Report-only** mode.

This allowed the policy to be evaluated safely without immediately enforcing access restrictions.

![Conditional Access Report-Only Evaluation](02-screenshots/16-conditional-access-report-only-evaluation.png)

This demonstrated a safer administrative workflow:

```text
Design
  â†“
Configure
  â†“
Report-only
  â†“
Evaluate
  â†“
Validate
  â†“
Enforce only when approved
```

---

## 10. Microsoft Entra Device Identity

Deployed a Windows 11 Enterprise endpoint named:

```text
CLOUDCLIENT01
```

The device was Microsoft Entra joined using a standard organizational identity.

Local validation with:

```powershell
dsregcmd /status
```

confirmed:

```text
AzureAdJoined : YES
DomainJoined  : NO
```

The device was also verified in the Microsoft Entra admin center.

![Microsoft Entra Joined Device](02-screenshots/17-microsoft-entra-joined-cloudclient01.png)

The lab also demonstrated that Microsoft Entra joining a device does not automatically mean the device is managed by Microsoft Intune.

---

## 11. Audit Logs and Microsoft 365 Service Health

Used Microsoft Entra audit logs to investigate administrative and synchronization activity.

![Microsoft Entra Audit Log](02-screenshots/19-entra-audit-log-hybrid-user-update.png)

Microsoft 365 Service Health was also used to distinguish user-specific troubleshooting from Microsoft-side service incidents.

![Microsoft 365 Service Health](02-screenshots/20-m365-service-health-incident-investigation.png)

---

## 12. Microsoft Graph PowerShell

Installed and used the Microsoft Graph PowerShell SDK for repeatable Microsoft 365 and Entra administration.

Tasks included:

* Retrieving users
* Reviewing account state
* Reviewing group memberships
* Inspecting Microsoft 365 licensing
* Performing a controlled user-property update
* Validating the resulting Entra audit event

![Microsoft Graph PowerShell Queries](02-screenshots/21-graph-powershell-user-group-license-query.png)

A controlled PowerShell update was then correlated with its corresponding Microsoft Entra audit record.

![Graph PowerShell Audit Validation](02-screenshots/22-graph-powershell-user-update-audit-verification.png)

---

# Hybrid Identity Implementation

The final stage connected the existing on-premises Active Directory environment with Microsoft Entra ID using **Microsoft Entra Connect Sync**.

The hybrid configuration used:

* Microsoft Entra Connect Sync
* Password Hash Synchronization
* Controlled pilot-group synchronization
* Existing cloud-user matching
* Synchronization validation
* Source-of-authority troubleshooting

The entire on-premises directory was intentionally **not** synchronized.

Instead, a controlled pilot scope was used for the four synthetic employee identities.

![Controlled Hybrid User Rollout](02-screenshots/24-controlled-hybrid-user-rollout.png)

---

## Source of Authority

Hybrid identity introduced an important administrative distinction:

```text
Cloud-only identity
        â†“
Cloud-managed attributes

Synchronized identity
        â†“
Certain attributes mastered on-premises
        â†“
Microsoft Entra Connect
        â†“
Microsoft Entra ID
```

The lab demonstrated how identity administrators must determine the authoritative source before modifying a synchronized attribute.

![Hybrid vs Cloud Identity](02-screenshots/23-hybrid-vs-cloud-identity-source-of-authority.png)

---

# Troubleshooting Experience

Real issues investigated during the project included:

* Disabled user authentication failure
* Entra sign-in error investigation
* Password and session troubleshooting
* Missing Microsoft 365 license
* Missing Exchange mailbox due to licensing state
* SharePoint authorization failure
* Stale browser/session behavior after permission restoration
* Teams policy behavior
* Microsoft 365 service-health investigation
* Microsoft Graph PowerShell configuration issues
* Hybrid identity matching
* Duplicate synchronized identity remediation
* Attribute source-of-authority issues
* Synchronization validation

The general support methodology used throughout the project was:

```text
Verify
  â†“
Investigate
  â†“
Identify Cause
  â†“
Remediate
  â†“
Validate
  â†“
Document
  â†“
Close or Escalate
```

---

# Enterprise Help Desk Capstone

The final phase applied the technical work to common enterprise support workflows.

### Joiner

```text
Request
â†’ Authorization
â†’ Identity
â†’ Attributes
â†’ Groups
â†’ Licensing
â†’ Services
â†’ Security
â†’ Validation
â†’ Documentation
```

### Mover

```text
Approved role change
â†’ Review existing access
â†’ Update authoritative attributes
â†’ Grant required new access
â†’ Remove obsolete access
â†’ Validate
â†’ Document
```

### Leaver

```text
Authorized termination
â†’ Disable/block access
â†’ Revoke sessions
â†’ Remove privileged access
â†’ Preserve business data
â†’ Reclaim licenses
â†’ Validate
â†’ Document
```

The lab emphasized disabling and preserving data according to policy rather than immediately deleting identities.


## Documentation

A consolidated project report is available in [`03-reports/microsoft-365-entra-it-support-lab-report.md`](03-reports/microsoft-365-entra-it-support-lab-report.md).
Detailed implementation and troubleshooting documentation is available in [`01-docs`](01-docs).

| Phase | Documentation                                                                                                     |
| ----- | ----------------------------------------------------------------------------------------------------------------- |
| 1     | [Microsoft 365 Lab Environment](01-docs/01-microsoft-365-lab-environment.md)                                      |
| 2     | [Microsoft Entra ID Fundamentals](01-docs/02-entra-id-fundamentals.md)                                            |
| 3     | [Cloud User Administration](01-docs/03-cloud-user-administration.md)                                              |
| 4     | [Groups and Access Management](01-docs/04-groups-access-management.md)                                            |
| 5     | [Licensing and Service Provisioning](01-docs/05-licensing-service-provisioning.md)                                |
| 6     | [User Support, Troubleshooting, and Least Privilege](01-docs/06-user-support-troubleshooting-least-privilege.md)  |
| 7     | [Teams, SharePoint, and OneDrive Administration](01-docs/07-teams-sharepoint-onedrive-administration.md)          |
| 8     | [Conditional Access and Device Identity](01-docs/08-conditional-access-device-identity.md)                        |
| 9     | [Monitoring, PowerShell, and Hybrid Identity](01-docs/09-monitoring-powershell-hybrid-identity.md)                |
| 10    | [Enterprise Help Desk Capstone and Final Validation](01-docs/10-enterprise-helpdesk-capstone-final-validation.md) |

---

# Repository Structure

```text
microsoft-365-entra-it-support-lab/
â”‚
â”œâ”€â”€ 01-docs/
â”‚   â”œâ”€â”€ 01-microsoft-365-lab-environment.md
â”‚   â”œâ”€â”€ 02-entra-id-fundamentals.md
â”‚   â”œâ”€â”€ 03-cloud-user-administration.md
â”‚   â”œâ”€â”€ 04-groups-access-management.md
â”‚   â”œâ”€â”€ 05-licensing-service-provisioning.md
â”‚   â”œâ”€â”€ 06-user-support-troubleshooting-least-privilege.md
â”‚   â”œâ”€â”€ 07-teams-sharepoint-onedrive-administration.md
â”‚   â”œâ”€â”€ 08-conditional-access-device-identity.md
â”‚   â”œâ”€â”€ 09-monitoring-powershell-hybrid-identity.md
â”‚   â””â”€â”€ 10-enterprise-helpdesk-capstone-final-validation.md
â”‚
â”œâ”€â”€ 02-screenshots/
â”œâ”€â”€ 03-reports/
â”‚   â””â”€â”€ microsoft-365-entra-it-support-lab-report.md
â”‚
â”œâ”€â”€ .gitignore
â””â”€â”€ README.md
```

---

# Skills Demonstrated

This project demonstrates practical experience with:

**Microsoft 365 Administration Â· Microsoft Entra ID Â· Identity & Access Management Â· User Administration Â· Group Management Â· Microsoft 365 Licensing Â· Exchange Online Â· Microsoft Teams Â· SharePoint Online Â· OneDrive Â· Authentication Â· MFA Â· RBAC Â· Least Privilege Â· Conditional Access Â· Sign-In Logs Â· Audit Logs Â· Microsoft Graph PowerShell Â· Microsoft Entra Device Identity Â· Microsoft Entra Connect Sync Â· Password Hash Synchronization Â· Hybrid Identity Â· Source of Authority Â· Troubleshooting Â· Joiner-Mover-Leaver Â· Help Desk Documentation**

---

# Security and Privacy

This project was built in an isolated lab environment using fictional employee identities and synthetic business data.

Public documentation intentionally excludes:

* Passwords
* Temporary credentials
* MFA secrets and QR codes
* Authentication tokens
* Recovery information
* Personal contact information
* Payment and billing information
* Sensitive tenant identifiers not required to demonstrate the lab


---

## What I Learned

- Microsoft 365 troubleshooting requires separating **identity, authentication, authorization, licensing, service provisioning, policy, and application health** rather than treating every access problem as a password issue.
- Successful authentication does not automatically mean a user is authorized for a resource or licensed for a Microsoft 365 service.
- Entra sign-in and audit logs provide stronger troubleshooting evidence than relying only on the user's visible error message.
- Administrative access should follow **least privilege**; routine Help Desk work does not require Global Administrator permissions.
- Conditional Access policies should be tested safely, such as with **Report-only mode**, before enforcement.
- Microsoft Entra device identity and device management are different concepts; an Entra-joined device is not automatically Intune-managed.
- In hybrid identity, administrators must understand **source of authority** before changing synchronized attributes.
- Controlled pilot synchronization is safer than immediately synchronizing an entire production-style directory.
- Identity matching and synchronization problems should be investigated before deleting or recreating accounts.
- Microsoft Graph PowerShell provides a repeatable way to investigate and administer Microsoft 365 while leaving an auditable record of administrative changes.


---

# Project Outcome

This project progressed from basic Microsoft 365 cloud-user administration into a broader enterprise identity and IT Support environment.

It provided hands-on experience troubleshooting user access across multiple layers:

```text
Identity
â†’ Authentication
â†’ Authorization
â†’ Licensing
â†’ Service Provisioning
â†’ Policy
â†’ Device Identity
â†’ Application
â†’ Logs
â†’ Hybrid Synchronization
```

Together with the Active Directory IT Support Lab, this project demonstrates experience across both traditional on-premises Microsoft identity infrastructure and modern Microsoft 365 / Microsoft Entra cloud administration.

---

## Project Status

**COMPLETE**

All planned implementation, troubleshooting, validation, and documentation objectives for this project have been completed.



