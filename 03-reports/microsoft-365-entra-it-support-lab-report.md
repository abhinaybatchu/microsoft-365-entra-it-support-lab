# Microsoft 365, Entra ID & Hybrid Identity IT Support Lab — Project Report

## Executive Summary

This project built and administered a Microsoft 365 enterprise lab designed around realistic IT Support, Service Desk, identity, access-management, and hybrid-identity scenarios.

The environment began with Microsoft Entra cloud identities and Microsoft 365 administration and later expanded into a controlled hybrid architecture connecting an existing on-premises Active Directory environment to Microsoft Entra ID through Microsoft Entra Connect Sync.

The project covered:

- Microsoft 365 tenant administration
- Microsoft Entra ID
- Cloud user administration
- Security groups and group-based access
- Microsoft 365 Business Premium licensing
- Exchange Online
- Microsoft Teams
- SharePoint Online
- OneDrive
- Authentication troubleshooting
- Microsoft Entra sign-in logs
- Microsoft Entra audit logs
- Role-Based Access Control
- Least-privilege Help Desk administration
- Conditional Access evaluation
- Microsoft Entra device identity
- Microsoft Graph PowerShell
- Microsoft 365 Service Health
- Microsoft Entra Connect Sync
- Password Hash Synchronization
- Controlled hybrid identity synchronization
- Identity matching
- Source-of-authority administration
- Duplicate identity remediation
- Joiner-Mover-Leaver workflows
- Ticket documentation and escalation methodology

The lab used only synthetic employees, synthetic organizational data, and controlled test scenarios.

The project was designed to demonstrate practical skills relevant to entry-level:

- IT Support
- Service Desk
- Microsoft 365 Support
- IAM Support
- Junior Systems Administration
- Security Support

---

# 1. Project Objectives

The primary objectives were to:

1. Build a realistic Microsoft 365 cloud administration environment.
2. Understand Microsoft Entra ID identity administration.
3. Practice common user and access-management workflows.
4. Understand Microsoft 365 licensing and service provisioning.
5. Troubleshoot authentication, authorization, licensing, application, and session problems separately.
6. Practice Microsoft Teams, SharePoint, OneDrive, and Exchange administration.
7. Apply Microsoft Entra RBAC and least privilege.
8. Evaluate Conditional Access safely before enforcement.
9. Understand Microsoft Entra device identity.
10. Use Microsoft Graph PowerShell for repeatable administration.
11. Use audit logs and Service Health during troubleshooting.
12. Integrate an existing Active Directory environment with Microsoft Entra ID.
13. Implement Password Hash Synchronization.
14. Perform a controlled hybrid identity rollout.
15. Troubleshoot source-of-authority and identity-matching problems.
16. Apply the technical environment to enterprise Help Desk Joiner-Mover-Leaver workflows.
17. Produce professional portfolio evidence without exposing credentials or personal information.

---

# 2. Lab Environment

## 2.1 Fictional Organization

```text
Organization:
Abhinay Labs
```

All employee identities and business scenarios used in the lab were synthetic.

---

## 2.2 Microsoft Cloud Environment

```text
Microsoft 365 Tenant:
abhinaylabs.onmicrosoft.com

Subscription:
Microsoft 365 Business Premium Trial

Microsoft Entra:
Microsoft Entra ID P1
```

Cloud services used included:

- Microsoft Entra ID
- Microsoft 365 Admin Center
- Exchange Online
- Microsoft Teams
- SharePoint Online
- OneDrive
- Microsoft Graph PowerShell
- Microsoft 365 Service Health

---

## 2.3 On-Premises Environment

The project extended the existing Active Directory lab:

```text
Domain:
abhinaylabs.internal
```

Primary systems included:

```text
DC01
Primary Active Directory Domain Controller / DNS

DC02
Additional Active Directory Domain Controller / DNS

SYNC01
Microsoft Entra Connect Sync Server

CLIENT01
Traditional Active Directory domain-joined Windows workstation
```

---

## 2.4 Cloud-First Endpoint

A separate Windows 11 Enterprise system was deployed:

```text
CLOUDCLIENT01
```

Its final device state was:

```text
Microsoft Entra joined:
Yes

Traditional AD domain joined:
No
```

This endpoint remained separate from CLIENT01 so that traditional and cloud-first device identity models could be compared.

---

# 3. Final Architecture

```text
                    ABHINAY LABS
                         |
          +--------------+--------------+
          |                             |
          |                             |
   ON-PREMISES                     MICROSOFT CLOUD
          |                             |
          |                             |
  abhinaylabs.internal         abhinaylabs.onmicrosoft.com
          |                             |
          |                             |
      +---+---+                   Microsoft Entra ID
      |       |                         |
     DC01    DC02                       +-- Users
      |       |                         +-- Security Groups
      +---+---+                         +-- Admin Roles
          |                             +-- Authentication
          |                             +-- Conditional Access
          |                             +-- Sign-In Logs
          |                             +-- Audit Logs
          |                             +-- Device Identity
          |
   Active Directory
          |
          +-- David Miller
          +-- Elena Rivera
          +-- Joseph Daniel
          +-- Pauline Hudson
          |
          v
        SYNC01
          |
 Microsoft Entra Connect Sync
          |
 Password Hash Synchronization
          |
          +---------------------------->
                                        |
                                Microsoft Entra ID
                                        |
                         +--------------+--------------+
                         |              |              |
                     Exchange         Teams        SharePoint
                         |              |              |
                       Outlook          |           OneDrive
                                        |
                                  Microsoft 365


ENDPOINT IDENTITY MODELS
------------------------

CLIENT01
    |
    +-- Active Directory domain joined
    +-- abhinaylabs.internal
    +-- Not Hybrid Microsoft Entra joined


CLOUDCLIENT01
    |
    +-- Microsoft Entra joined
    +-- AzureAdJoined : YES
    +-- DomainJoined : NO
```

---

# 4. Synthetic Employee Identities

The lab used four primary fictional employees.

| Employee       | Username  | Department      | Final Authoritative Job Title |
| -------------- | --------- | --------------- | ----------------------------- |
| David Miller   | `dmiller` | Human Resources | HR Coordinator                |
| Elena Rivera   | `erivera` | Finance         | Financial Analyst             |
| Joseph Daniel  | `jdaniel` | Sales           | Sales Representative          |
| Pauline Hudson | `phudson` | IT              | IT Support Specialist         |

Cloud UPN format:

```text
username@abhinaylabs.onmicrosoft.com
```

Examples:

```text
dmiller@abhinaylabs.onmicrosoft.com
erivera@abhinaylabs.onmicrosoft.com
jdaniel@abhinaylabs.onmicrosoft.com
phudson@abhinaylabs.onmicrosoft.com
```

The identities were originally created directly in Microsoft Entra ID.

Later, the existing cloud identities were matched to their corresponding on-premises Active Directory identities during the controlled hybrid rollout.

---

# 5. Microsoft Entra User Administration

The project began with direct Microsoft Entra administration.

Tasks included:

- Creating cloud users
- Configuring User Principal Names
- Setting job titles
- Setting departments
- Setting company information
- Setting usage location
- Reviewing Member user type
- Resetting passwords
- Disabling users
- Re-enabling users
- Reviewing bulk administration
- Validating account state

A central concept was that these properties represent separate administrative layers.

For example:

```text
User exists
      ≠
User has Microsoft 365 license

User enabled
      ≠
User authorized for every resource

User authenticated
      ≠
User has every required application
```

---

# 6. Group and Access Management

Microsoft Entra security groups were created for departmental and job-function access.

```text
SG-HR-Users
SG-Finance-Users
SG-Sales-Users
SG-IT-Users
SG-IT-Helpdesk
```

Initial membership included:

```text
David Miller
    → SG-HR-Users

Elena Rivera
    → SG-Finance-Users

Joseph Daniel
    → SG-Sales-Users

Pauline Hudson
    → SG-IT-Users
    → SG-IT-Helpdesk
```

The project emphasized:

```text
User
  ↓
Approved Security Group
  ↓
Resource Permission
```

rather than unnecessary direct user permissions.

It also demonstrated that:

```text
Security Group
      ≠
Microsoft Entra Administrative Role
```

For example, membership in:

```text
SG-IT-Helpdesk
```

did not automatically grant Pauline Microsoft Entra Helpdesk Administrator privileges.

---

# 7. Microsoft 365 Licensing & Service Provisioning

Microsoft 365 Business Premium was assigned in a controlled licensing scenario.

David Miller was used to validate the complete provisioning lifecycle.

```text
Microsoft Entra Identity
        ↓
Microsoft 365 Business Premium
        ↓
Service Entitlement
        ↓
Exchange Online Provisioning
        ↓
Mailbox Creation
        ↓
Microsoft 365 Workload Access
```

Validation included:

- Exchange Online mailbox
- Outlook
- Microsoft Teams
- SharePoint
- OneDrive
- Microsoft 365 web access

The project reinforced:

```text
License assigned
        ≠
Service automatically validated
```

Actual workload access was verified after provisioning.

---

# 8. Authentication Troubleshooting

A controlled account-state troubleshooting scenario was performed using David Miller.

User-facing symptoms included Microsoft 365 authentication problems.

Instead of immediately resetting the password, Microsoft Entra sign-in logs were investigated.

A relevant failed Outlook event recorded:

```text
Error Code:
50057

Failure Reason:
The user account is disabled.
```

The troubleshooting sequence was:

```text
Reported authentication issue
        ↓
Verify identity
        ↓
Review Microsoft Entra sign-in logs
        ↓
Locate failed authentication
        ↓
Error 50057
        ↓
Disabled account identified
        ↓
Authorized remediation
        ↓
Validate
```

This demonstrated that sign-in logs provide stronger evidence than relying only on the user-facing error message.

![Microsoft Entra Sign-In Troubleshooting](../02-screenshots/09-entra-signin-log-troubleshooting.png)

---

# 9. Licensing vs Authentication Troubleshooting

Elena Rivera was used for a separate Microsoft 365 troubleshooting scenario.

Elena:

```text
Had a valid Microsoft Entra identity
        +
Could authenticate
```

but initially did not have the required Microsoft 365 license or Exchange mailbox.

Outlook produced an error containing:

```text
OwaUserHasNoMailboxAndNoLicenseAssignedException
```

The actual troubleshooting chain was:

```text
Identity exists
      ↓
Account enabled
      ↓
Authentication succeeds
      ↓
Outlook fails
      ↓
Check licensing
      ↓
Required license absent
      ↓
Exchange mailbox absent
```

This reinforced:

```text
Authentication success
        ≠
Microsoft 365 service entitlement
```

---

# 10. SharePoint Authorization Troubleshooting

The Finance SharePoint environment was used to test group-based authorization.

The approved access path was:

```text
Elena Rivera
      ↓
SG-Finance-Users
      ↓
Finance Members
      ↓
Finance SharePoint Site
```

Elena initially had access.

Her membership in:

```text
SG-Finance-Users
```

was intentionally removed.

The result was:

```text
Authentication:
Successful

Authorization:
Failed
```

SharePoint displayed:

```text
You need access
```

and effective permission checking showed no Finance site access.

![SharePoint Access Denied](../02-screenshots/11-sharepoint-access-denied.png)

The correct remediation was to restore the approved Finance security-group membership rather than create a direct user permission.

After restoring the group, stale browser/session state temporarily continued to show the denial.

Clearing the relevant SharePoint site cookies refreshed the session and restored access.

This produced two distinct troubleshooting lessons:

```text
Stage 1:
Backend authorization problem

Stage 2:
Stale client/session state
```

The backend access model was corrected first.

Client cleanup was performed only afterward.

---

# 11. Exchange Online Administration

Exchange Online administration included:

- Mailbox provisioning
- Mailbox validation
- Email testing
- Internal mail forwarding
- Forwarding removal
- Post-change validation

Elena's mailbox was temporarily configured to forward messages to David while retaining delivery to Elena.

The configuration was tested and then removed.

This demonstrated that mailbox forwarding can be:

```text
Legitimate administrative feature
```

but may also become:

```text
Security investigation indicator
```

if configured unexpectedly.

Unexpected forwarding should therefore be reviewed in the context of authorization and possible account compromise.

---

# 12. Least-Privilege Administration

Pauline Hudson was used as the synthetic Help Desk technician.

Rather than assigning unrestricted tenant access, Pauline received:

```text
Helpdesk Administrator
```

Her normal group membership remained separately represented through:

```text
SG-IT-Users
SG-IT-Helpdesk
```

The distinction was:

```text
Security Group
      ↓
Organizational / access membership

Microsoft Entra Role
      ↓
Administrative privilege
```

The Helpdesk Administrator role was tested against both allowed support tasks and restricted higher-privilege operations.

The goal was to demonstrate:

```text
Required Help Desk capability
        +
No unnecessary Global Administrator access
```

---

# 13. Teams Administration

A private Finance Team was created.

The environment included:

```text
Finance Team
      |
      +-- Elena Rivera
      |      Owner
      |
      +-- Budget and Reporting
             Standard Channel
```

Administrative tasks included:

- Team creation
- Owner assignment
- Member lifecycle testing
- Standard-channel administration
- Access validation

David Miller was temporarily added and later removed to validate the membership lifecycle:

```text
Grant
  ↓
Validate
  ↓
Revoke
  ↓
Validate
```

---

# 14. Teams Messaging Policy

A custom Teams policy was created:

```text
Finance-Messaging-Policy
```

The policy was assigned directly to Elena Rivera for controlled testing.

Message-editing behavior was changed and validated from the user perspective.

The test demonstrated that a Teams feature issue can originate from:

```text
Administrative Policy
```

rather than:

```text
Broken Teams client
```

The user was returned to the appropriate policy state after testing.

---

# 15. Teams and SharePoint Integration

A Finance document was used to validate the relationship between Teams and SharePoint.

```text
Finance Team
      ↓
Budget and Reporting
      ↓
September Budget Notes.docx
      ↓
SharePoint Document Library
```

The same file was verified through both Teams and its SharePoint-backed storage.

This demonstrated:

```text
Teams standard-channel files
        ↓
Stored in SharePoint
```

Understanding this relationship is important because a Teams file-access issue may actually involve SharePoint permissions or storage.

---

# 16. OneDrive Administration

OneDrive administration included:

- Storage review
- Sharing review
- Retention review
- Administrative file access

A controlled business-continuity scenario was performed using David Miller's OneDrive.

The administrator used supported administrative access to reach:

```text
HR-Handover-Notes.docx
```

without using David's password.

This demonstrated an important enterprise principle:

```text
Authorized business-data access
        ↓
Use supported administrative mechanism
        ↓
Do not request employee credentials
```

OneDrive retention behavior was also reviewed as part of future offboarding considerations.

---

# 17. Conditional Access

A Conditional Access policy was configured:

```text
CA-Require-MFA-Finance
```

The policy targeted Elena Rivera in the Finance scenario for Office 365 Exchange Online and was intentionally left in:

```text
Report-only
```

mode.

This allowed the policy to be evaluated without enforcing the configured access requirement.

![Conditional Access Report-Only Evaluation](../02-screenshots/16-conditional-access-report-only-evaluation.png)

The project demonstrated the safer workflow:

```text
Design
  ↓
Configure
  ↓
Report-only
  ↓
Evaluate
  ↓
Validate
  ↓
Enforce only after approval
```

The lab does not claim that this Conditional Access policy was placed into production-style enforcement.

---

# 18. Microsoft Entra Device Identity

A Windows 11 Enterprise endpoint named:

```text
CLOUDCLIENT01
```

was joined directly to Microsoft Entra ID.

Local validation used:

```cmd
dsregcmd /status
```

Important results included:

```text
AzureAdJoined : YES
EnterpriseJoined : NO
DomainJoined : NO
Device Name : CLOUDCLIENT01
```

The user state also showed:

```text
WorkplaceJoined : NO
WamDefaultSet : YES
AzureAdPrt : YES
```

This confirmed that the device was:

```text
Microsoft Entra joined
```

and not:

```text
Traditional AD domain joined
```

or:

```text
Hybrid Microsoft Entra joined
```

![Microsoft Entra Joined CLOUDCLIENT01](../02-screenshots/17-microsoft-entra-joined-cloudclient01.png)

The project also demonstrated:

```text
Microsoft Entra joined
        ≠
Automatically Intune managed
```

No claim of full Intune deployment is made by this project.

---

# 19. Monitoring and Microsoft 365 Service Health

Microsoft Entra audit logs were used to investigate administrative and synchronization activity.

Microsoft 365 Service Health was also reviewed to determine whether reported problems could be caused by Microsoft-side incidents or advisories.

A useful support distinction became:

```text
Single-user issue
        ↓
Investigate user / device / configuration

Multiple-user or service-wide symptoms
        ↓
Consider tenant configuration
        +
Microsoft 365 Service Health
```

This prevents unnecessary user-side remediation during Microsoft service problems.

---

# 20. Microsoft Graph PowerShell

Microsoft Graph PowerShell was used for repeatable Microsoft Entra and Microsoft 365 administration.

Examples included:

### User Query

```powershell
Get-MgUser -UserId "dmiller@abhinaylabs.onmicrosoft.com" -Property DisplayName,JobTitle |
Select-Object DisplayName,JobTitle
```

### User Property Update

```powershell
Update-MgUser `
    -UserId "jdaniel@abhinaylabs.onmicrosoft.com" `
    -JobTitle "Sales Support Specialist"
```

### Licensing Query

```powershell
Get-MgSubscribedSku |
Select-Object SkuPartNumber,ConsumedUnits,@{Name="EnabledUnits";Expression={$_.PrepaidUnits.Enabled}}
```

The Joseph Daniel job-title update was then verified through Microsoft Entra audit evidence.

![Microsoft Graph PowerShell Audit Verification](../02-screenshots/22-graph-powershell-user-update-audit-verification.png)

This demonstrated:

```text
PowerShell Change
      ↓
Microsoft Graph
      ↓
Microsoft Entra
      ↓
Audit Evidence
```

---

# 21. Hybrid Identity Implementation

The project progressed beyond cloud-only identity administration by implementing Microsoft Entra Connect Sync on:

```text
SYNC01
```

The final architecture used:

```text
On-Premises Active Directory
        ↓
Microsoft Entra Connect Sync
        ↓
Password Hash Synchronization
        ↓
Microsoft Entra ID
        ↓
Microsoft 365
```

The implementation used:

```text
Source Anchor:
mS-DS-ConsistencyGuid
```

and:

```text
Authentication Method:
Password Hash Synchronization
```

---

# 22. Password Hash Synchronization

Password Hash Synchronization was enabled for the controlled hybrid deployment.

The conceptual process was:

```text
On-premises password
        ↓
Active Directory password hash
        ↓
Additional one-way derived hash
        ↓
Microsoft Entra ID
```

Plaintext passwords were not synchronized.

The project does not claim that Microsoft Entra receives a reversible copy of the user's plaintext Active Directory password.

---

# 23. Controlled Pilot Synchronization

The project deliberately avoided a whole-directory synchronization.

A controlled pilot group was used:

```text
Entra-Sync-Pilot
```

The final synchronized users were:

```text
David Miller
Elena Rivera
Joseph Daniel
Pauline Hudson
```

The project intentionally did **not** synchronize:

- The complete Active Directory directory
- On-premises AD security groups
- CLIENT01
- Other computer objects

The cloud security groups remained cloud-managed.

This limited scope made synchronization easier to understand, test, and troubleshoot.

---

# 24. Existing Cloud Account Matching

The users already existed in Microsoft Entra ID before hybrid synchronization was implemented.

The objective was therefore:

```text
Existing On-Premises User
        ↓
Microsoft Entra Connect
        ↓
Existing Cloud User
```

rather than:

```text
Existing Cloud User
        +
Second Unrelated Hybrid User
```

David Miller was used as the initial pilot identity.

After UPN alignment and synchronization, the existing cloud identity became synchronized.

This demonstrated preservation of the existing cloud account during the transition to hybrid identity.

---

# 25. Source of Authority

Hybrid identity introduced the concept of:

```text
Source of Authority
```

For cloud-only identities:

```text
Microsoft Entra ID
        ↓
Cloud-managed attributes
```

For synchronized attributes:

```text
Active Directory
        ↓
Microsoft Entra Connect
        ↓
Microsoft Entra ID
```

The project demonstrated this directly when previously populated cloud attributes became blank after synchronization because the corresponding authoritative on-premises attributes were empty.

The correct remediation was:

```text
Correct Active Directory attribute
        ↓
Run synchronization
        ↓
Validate Microsoft Entra result
```

rather than repeatedly editing the synchronized attribute in the cloud.

---

# 26. Final Authoritative Attributes

The final Active Directory values used for synchronized users included:

### David Miller

```text
Job Title:
HR Coordinator

Department:
Human Resources

Company:
Abhinay Labs
```

### Elena Rivera

```text
Job Title:
Financial Analyst

Department:
Finance

Company:
Abhinay Labs
```

### Joseph Daniel

```text
Job Title:
Sales Representative

Department:
Sales

Company:
Abhinay Labs
```

### Pauline Hudson

```text
Job Title:
IT Support Specialist

Department:
IT

Company:
Abhinay Labs
```

These values became authoritative for the corresponding synchronized attributes.

---

# 27. Joseph Daniel — Cloud vs Hybrid Administration

Before Joseph became synchronized, Microsoft Graph PowerShell was used to update his cloud job title to:

```text
Sales Support Specialist
```

Later, after hybrid synchronization, Active Directory became authoritative for the synchronized job-title attribute.

The on-premises value was:

```text
Sales Representative
```

This demonstrated an important hybrid administration principle:

```text
Correct administrative location depends on source of authority
```

A command that was valid for a cloud-only identity may no longer be the correct long-term management method after synchronization.

---

# 28. Microsoft Entra Connect Health

The synchronization scheduler was validated using:

```powershell
Get-ADSyncScheduler |
Select-Object SyncCycleEnabled,
              StagingModeEnabled,
              SchedulerSuspended,
              SyncCycleInProgress,
              CurrentlyEffectiveSyncCycleInterval
```

The final intended operational state was:

```text
SyncCycleEnabled                    : True
StagingModeEnabled                  : False
SchedulerSuspended                  : False
SyncCycleInProgress                 : False
CurrentlyEffectiveSyncCycleInterval : 00:30:00
```

The Windows synchronization service was validated with:

```powershell
Get-Service ADSync |
Select-Object Name,Status,StartType
```

Final state:

```text
ADSync
Running
Automatic
```

Controlled delta synchronization was triggered using:

```powershell
Start-ADSyncSyncCycle -PolicyType Delta
```

---

# 29. Troubleshooting Case Study — Pauline Duplicate Identity

The most significant hybrid identity troubleshooting scenario occurred with Pauline Hudson.

The intended cloud identity already existed:

```text
phudson@abhinaylabs.onmicrosoft.com
```

and held:

```text
Helpdesk Administrator
```

During synchronization, the privileged cloud identity did not automatically match as expected.

An unintended synchronized identity appeared:

```text
phudson1975@abhinaylabs.onmicrosoft.com
```

The temporary state became:

```text
One Employee
     |
     +-- phudson@...
     |      Existing Cloud Identity
     |      Helpdesk Administrator
     |
     +-- phudson1975@...
            Unintended Synchronized Duplicate
```

---

# 30. Pauline Investigation

The duplicate was not immediately deleted.

The investigation included:

- Verifying the legitimate original identity
- Verifying the incoming on-premises identity
- Checking UPN alignment
- Reviewing synchronization scope
- Reviewing existing administrative privilege
- Determining which object should be preserved

The conflict was associated with protection around matching the incoming synchronized identity to an existing privileged cloud account.

This was treated as an identity-matching problem rather than simply a naming problem.

---

# 31. Pauline Remediation

The remediation workflow was:

```text
Verify legitimate original identity
        ↓
Temporarily remove Helpdesk Administrator
        ↓
Remove Pauline from pilot synchronization scope
        ↓
Run synchronization
        ↓
Unintended synchronized duplicate removed from active scope
        ↓
Permanently remove only the unintended duplicate
        ↓
Confirm original phudson identity remains
        ↓
Re-add Pauline to controlled sync scope
        ↓
Run synchronization
        ↓
Existing phudson identity matches
        ↓
Confirm one Pauline identity
        ↓
Restore Helpdesk Administrator
        ↓
Validate final state
```

This preserved the intended employee identity rather than deleting and recreating the legitimate account.

---

# 32. Pauline Final State

The final intended identity was:

```text
Pauline Hudson
phudson@abhinaylabs.onmicrosoft.com
```

with:

```text
On-premises synchronization:
Enabled

Cloud administrative role:
Helpdesk Administrator
```

This demonstrated that a hybrid identity can contain both:

```text
On-premises-mastered attributes
```

and:

```text
Cloud-managed administrative properties
```

---

# 33. Final Hybrid Rollout

The final controlled synchronization contained exactly four intended employee identities:

```text
David Miller
Elena Rivera
Joseph Daniel
Pauline Hudson
```

![Controlled Hybrid User Rollout](../02-screenshots/24-controlled-hybrid-user-rollout.png)

The final scope did not include the entire Active Directory environment.

This limitation is intentional and forms part of the project's risk-controlled design.

---

# 34. Joiner Workflow

The project concluded by applying the environment to enterprise employee lifecycle scenarios.

A Joiner workflow was modeled as:

```text
Receive onboarding request
        ↓
Verify requester and approval
        ↓
Confirm job role
        ↓
Provision identity
        ↓
Configure organizational attributes
        ↓
Assign approved groups
        ↓
Assign required Microsoft 365 license
        ↓
Validate service provisioning
        ↓
Apply security requirements
        ↓
Validate end-user access
        ↓
Document
        ↓
Close / Escalate
```

The project deliberately avoided the shortcut:

```text
"Copy everything another employee has."
```

Access should instead be based on the approved job requirement.

---

# 35. Mover Workflow

Joseph Daniel was used conceptually for a:

```text
Sales → Finance
```

transfer scenario.

The workflow included:

```text
Verify approved transfer
        ↓
Confirm effective date
        ↓
Update authoritative attributes
        ↓
Grant approved Finance access
        ↓
Remove obsolete Sales-only access
        ↓
Review license and services
        ↓
Validate
        ↓
Document
```

This reinforced the risk of:

```text
Privilege Creep
```

where users accumulate old permissions after changing roles.

---

# 36. Leaver Workflow

The offboarding model used:

```text
Verify authorized termination
        ↓
Confirm effective time
        ↓
Block sign-in
        ↓
Revoke sessions
        ↓
Remove privileged / unnecessary access
        ↓
Preserve required mailbox / OneDrive data
        ↓
Transfer business data according to policy
        ↓
Reclaim license
        ↓
Manage authoritative AD identity
        ↓
Validate access blocked
        ↓
Document
```

A central principle was:

> Disable first; do not immediately delete.

This preserves time for legitimate business, retention, investigation, and data-transfer requirements.

---

# 37. Enterprise Troubleshooting Methodology

The project produced a reusable Help Desk methodology:

```text
VERIFY
  ↓
INVESTIGATE
  ↓
REMEDIATE
  ↓
VALIDATE
  ↓
DOCUMENT
  ↓
CLOSE / ESCALATE
```

### Verify

Confirm:

- Correct user
- Correct requester
- Authorization
- Scope
- Affected service

### Investigate

Use appropriate evidence:

- User state
- Sign-in logs
- Audit logs
- Group membership
- Licensing
- Permissions
- Service Health
- Conditional Access
- Device state
- Source of authority
- Synchronization status

### Remediate

Correct the actual cause using the least disruptive authorized action.

### Validate

Confirm that the intended user or system state has actually been restored.

### Document

Record:

- Issue
- Scope
- Authorization
- Findings
- Root cause
- Actions
- Validation

### Close or Escalate

Close when validated.

Escalate when additional access, expertise, vendor support, security investigation, or infrastructure ownership is required.

---

# 38. Ticket Documentation Model

A reusable enterprise ticket structure was developed:

```text
Issue / Request
Requester / Authorization
Impact / Scope
Investigation
Findings / Root Cause
Actions Taken
Validation
Resolution
Escalation, if required
```

High-quality escalation should also include:

- Exact errors
- Relevant logs
- Screenshots where appropriate
- Troubleshooting already completed
- Results of those actions
- Reason escalation is necessary

The goal is to avoid low-value escalation notes such as:

```text
"Not working. Please check."
```

---

# 39. Security Controls Applied

The project applied several practical security principles.

## Least Privilege

The Help Desk user received:

```text
Helpdesk Administrator
```

instead of unrestricted Global Administrator access.

---

## Group-Based Access

Access was managed through appropriate groups rather than unnecessary direct user permissions.

---

## Safe Conditional Access Testing

Conditional Access was tested in:

```text
Report-only
```

mode before any enforcement claim.

---

## Controlled Hybrid Rollout

Only four intended users were synchronized.

The entire directory was not synchronized.

---

## Source-of-Authority Discipline

Synchronized attributes were corrected in the authoritative on-premises system.

---

## Privileged Identity Protection

Pauline's identity-matching conflict was investigated before deleting any account.

---

## Password Security

Password Hash Synchronization did not involve transferring plaintext passwords.

---

## Credential Privacy

Public portfolio material excludes:

- Passwords
- Temporary passwords
- MFA QR codes
- Authentication secrets
- Recovery credentials
- Tokens
- Personal contact details
- Billing information

---

# 40. Final Validation

The project concluded with a final environment review.

## Hybrid Users

Final intended synchronized identities:

```text
David Miller       PASS
Elena Rivera       PASS
Joseph Daniel      PASS
Pauline Hudson     PASS
```

---

## Pauline Duplicate

```text
phudson
Intended identity retained

phudson1975
Unintended duplicate removed
```

Status:

```text
PASS
```

---

## Help Desk Role

```text
Pauline Hudson
Helpdesk Administrator
```

Status:

```text
PASS
```

---

## Microsoft Entra Connect

```text
ADSync service:
Running

Startup:
Automatic

Scheduler:
Enabled

Staging:
Disabled

Scheduler suspended:
No

Normal sync interval:
30 minutes
```

Status:

```text
PASS
```

---

## Synchronization Scope

```text
Four intended users:
Synchronized

On-premises groups:
Not synchronized

CLIENT01:
Not synchronized

Complete AD environment:
Not synchronized
```

Status:

```text
PASS
```

---

## CLIENT01

```text
Traditional Active Directory domain joined:
Yes

Hybrid Microsoft Entra joined:
No
```

Status:

```text
PASS
```

---

## CLOUDCLIENT01

```text
Microsoft Entra joined:
Yes

DomainJoined:
No
```

Status:

```text
PASS
```

---

## Conditional Access

```text
CA-Require-MFA-Finance:
Report-only
```

Status:

```text
PASS
```

The project makes no claim of production enforcement.

---

# 41. Major Troubleshooting Cases

| Scenario                                          | Root Cause / Finding                                      | Resolution                                                                |
| ------------------------------------------------- | --------------------------------------------------------- | ------------------------------------------------------------------------- |
| David cannot authenticate to Outlook              | Entra sign-in event `50057` identified disabled account   | Validate account state and restore authorized state                       |
| Elena authenticates but Outlook fails             | No required license / Exchange mailbox                    | Correct licensing and provisioning layer                                  |
| Elena loses Finance SharePoint access             | Approved Finance group membership removed                 | Restore `SG-Finance-Users`                                                |
| SharePoint still denied after membership restored | Stale browser/session state                               | Correct backend first, then clear relevant site cookies                   |
| PowerShell command unavailable                    | Local Microsoft Graph module/session loading issue        | Validate/import module and reconnect                                      |
| Hybrid user attributes disappear                  | Blank authoritative AD attributes synchronized            | Correct AD attributes and delta sync                                      |
| Entra Connect scheduler not active                | `SyncCycleEnabled` observed false                         | Correct scheduler and revalidate                                          |
| Pauline receives duplicate synchronized identity  | Privileged cloud identity matching conflict               | Controlled scope/role remediation, remove only duplicate, resync original |
| Potential M365 service problem                    | Needed distinction between local and Microsoft-side issue | Review Microsoft 365 Service Health                                       |

---

# 42. Skills Demonstrated

## Microsoft 365 Administration

- Microsoft 365 Admin Center
- Microsoft 365 Business Premium
- License assignment
- Service provisioning
- Exchange Online
- Microsoft Teams
- SharePoint Online
- OneDrive

## Microsoft Entra ID

- User administration
- Group administration
- User Principal Names
- Account status
- Password support
- Sign-in logs
- Audit logs
- Administrative roles
- RBAC
- Conditional Access
- Device identity

## Identity & Access Management

- Authentication
- Authorization
- Group-based access
- Least privilege
- Joiner-Mover-Leaver
- Privilege-creep prevention
- Source of authority
- Hybrid identity
- Identity matching

## Troubleshooting

- Disabled-account authentication failures
- Sign-in error analysis
- Licensing failures
- Exchange mailbox provisioning
- SharePoint authorization
- Session/cookie troubleshooting
- Service Health investigation
- Hybrid identity conflicts
- Synchronization health
- Duplicate object remediation

## PowerShell

- Microsoft Graph PowerShell
- User queries
- User updates
- Licensing queries
- Entra Connect scheduler validation
- ADSync service validation
- Delta synchronization

## Windows / Device Identity

- Windows 11 Enterprise
- Microsoft Entra join
- `dsregcmd /status`
- Primary Refresh Token concepts
- Windows Web Account Manager
- AD domain join vs Entra join

---

# 43. Key Technical Lessons

The most important technical lessons from the project were:

1. Authentication, authorization, licensing, provisioning, policy, and application health are separate troubleshooting layers.
2. A successful sign-in does not guarantee authorization or Microsoft 365 service entitlement.
3. Microsoft Entra logs provide stronger evidence than relying solely on user-facing error messages.
4. Group-based permissions are easier to manage and review than unnecessary direct permissions.
5. Microsoft Entra administrative roles should follow least privilege.
6. Conditional Access should be evaluated safely before enforcement.
7. Microsoft Entra joining a Windows device does not automatically mean the device is Intune-managed.
8. Teams standard-channel files depend on SharePoint.
9. OneDrive administrative access should use supported administrative mechanisms rather than employee passwords.
10. Microsoft 365 Service Health should be considered when symptoms suggest a service-side issue.
11. PowerShell administration should still be validated and audited.
12. Hybrid identity requires understanding which system is authoritative for each property.
13. Synchronizing blank authoritative attributes can overwrite populated cloud values.
14. Identity matching should be investigated carefully before deleting duplicate objects.
15. Privileged cloud identities require additional care during hybrid matching.
16. Pilot synchronization reduces the risk and complexity of hybrid deployment.
17. A synchronized identity can contain both on-premises-mastered and cloud-managed properties.
18. Employee lifecycle administration must include both access assignment and access removal.
19. Offboarding should generally disable access before permanent deletion.
20. Every significant change should be followed by validation.

---

# 44. Enterprise Relevance

The lab reflects tasks commonly handled by:

- Service Desk analysts
- IT Support technicians
- Microsoft 365 administrators
- IAM support analysts
- Junior systems administrators
- Security support analysts

Typical enterprise tickets represented by this project include:

```text
"Reset my Microsoft 365 password."

"Why can't I sign in?"

"Outlook says I don't have a mailbox."

"I need access to the Finance SharePoint site."

"Please add this user to the Finance Team."

"Why can this user no longer edit Teams messages?"

"Can we access a former employee's OneDrive files?"

"Is Microsoft 365 experiencing an outage?"

"Why didn't the user's cloud profile update from AD?"

"Why are there two accounts for the same employee?"

"Is Microsoft Entra Connect synchronization working?"

"Employee changed departments. What access should be removed?"
```

The project therefore emphasized practical enterprise administration and troubleshooting rather than only theoretical Microsoft 365 knowledge.

---

# 45. Scope Limitations

To keep portfolio claims accurate, the project does **not** claim:

- Production Microsoft 365 administration
- Full Intune deployment
- Production Conditional Access enforcement
- Exchange Hybrid deployment
- Full Active Directory synchronization
- On-premises AD group synchronization
- Hybrid Microsoft Entra joining of CLIENT01
- Organization-wide MFA deployment
- Enterprise-scale user population
- Real employee or customer administration

The environment was a controlled home lab built with synthetic identities.

---

# 46. Documentation

Detailed phase-by-phase implementation documentation is available in:

```text
01-docs/
```

| Phase | Documentation                                                                                                      |
| ----- | ------------------------------------------------------------------------------------------------------------------ |
| 1     | [Microsoft 365 Lab Environment](../01-docs/01-microsoft-365-lab-environment.md)                                    |
| 2     | [Microsoft Entra ID Fundamentals](../01-docs/02-entra-id-fundamentals.md)                                          |
| 3     | [Cloud User Administration](../01-docs/03-cloud-user-administration.md)                                            |
| 4     | [Groups & Access Management](../01-docs/04-groups-access-management.md)                                            |
| 5     | [Licensing & Service Provisioning](../01-docs/05-licensing-service-provisioning.md)                                |
| 6     | [User Support, Troubleshooting & Least Privilege](../01-docs/06-user-support-troubleshooting-least-privilege.md)   |
| 7     | [Teams, SharePoint & OneDrive Administration](../01-docs/07-teams-sharepoint-onedrive-administration.md)           |
| 8     | [Conditional Access & Device Identity](../01-docs/08-conditional-access-device-identity.md)                        |
| 9     | [Monitoring, PowerShell & Hybrid Identity](../01-docs/09-monitoring-powershell-hybrid-identity.md)                 |
| 10    | [Enterprise Help Desk Capstone & Final Validation](../01-docs/10-enterprise-helpdesk-capstone-final-validation.md) |

---

# 47. Evidence Strategy

The repository contains 24 approved screenshots.

The screenshots are organized by the technical phase in which the work was performed.

The detailed phase documentation contains the complete evidence mapping.

This report intentionally includes only a small number of representative screenshots so that it remains readable as a professional project report rather than duplicating the entire evidence set.

Representative evidence included in this report demonstrates:

- Authentication troubleshooting
- SharePoint authorization troubleshooting
- Conditional Access evaluation
- Microsoft Entra device identity
- Microsoft Graph PowerShell auditing
- Controlled hybrid identity rollout

---

# 48. Project Outcome

The final project successfully demonstrated the progression from:

```text
Cloud Microsoft 365 Administration
                ↓
Identity and Access Administration
                ↓
Microsoft 365 Service Support
                ↓
Authentication and Authorization Troubleshooting
                ↓
Least-Privilege Administration
                ↓
Conditional Access and Device Identity
                ↓
Monitoring and PowerShell
                ↓
Hybrid Identity
                ↓
Enterprise Help Desk Lifecycle Workflows
```

The environment ultimately connected the existing Active Directory lab with Microsoft Entra ID through a controlled four-user Microsoft Entra Connect deployment while preserving the intended Microsoft 365 identities.

The project also produced several realistic troubleshooting cases that required identifying root cause rather than simply following scripted configuration steps.

---

# 49. Conclusion

This project developed practical experience administering Microsoft 365, Microsoft Entra ID, collaboration services, access controls, Windows cloud identity, PowerShell, and hybrid identity.

The strongest outcome was not simply the number of Microsoft technologies configured.

The project demonstrated a structured support methodology:

```text
Verify
  ↓
Investigate
  ↓
Remediate
  ↓
Validate
  ↓
Document
  ↓
Close / Escalate
```

The troubleshooting scenarios required separating identity, authentication, authorization, licensing, provisioning, policy, session state, service health, and source-of-authority problems.

The final hybrid deployment also demonstrated that enterprise identity administration requires careful matching, controlled synchronization scope, least privilege, and verification before destructive actions.

The completed lab provides portfolio evidence relevant to entry-level IT Support, Service Desk, Microsoft 365 Support, and IAM-focused roles.

---

## Project Status

**COMPLETE**

All planned implementation, troubleshooting, validation, and project-report objectives were completed in the controlled Abhinay Labs environment.

