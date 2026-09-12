# Phase 10 — Enterprise Help Desk Capstone & Final Validation

## 1. Objective

The objective of this phase was to combine the Microsoft 365, Microsoft Entra ID, Microsoft 365 workload, security, troubleshooting, PowerShell, and hybrid identity skills developed throughout the project into realistic enterprise Help Desk workflows.

The phase focused on:

- Joiner administration
- Mover administration
- Leaver administration
- Identity and access review
- Licensing and service decisions
- Authentication troubleshooting
- Microsoft 365 service troubleshooting
- Authorization troubleshooting
- Hybrid identity troubleshooting
- Duplicate identity troubleshooting
- Ticket documentation
- Escalation quality
- Final environment validation
- Final security and scope review

The goal was to move from individual technical tasks to a structured support mindset that could be applied to real enterprise tickets.

---

## 2. Enterprise Help Desk Methodology

The general support methodology used throughout the capstone was:

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
Close or Escalate
```

This workflow prevents support personnel from making configuration changes before understanding the request or problem.

---

## 3. Verify

Before making an administrative change, the technician should verify:

- The correct user
- The correct requester
- The legitimacy of the request
- Required authorization or approval
- The affected service or resource
- The scope and impact
- Any relevant timing requirements

Examples include:

```text
Password reset
        ↓
Verify the user and request first

New employee access
        ↓
Verify approved onboarding request

Department transfer
        ↓
Verify approved role change

Employee termination
        ↓
Verify authorized effective time
```

Technical ability does not replace authorization.

---

## 4. Investigate

After verification, the technician should determine the current state before changing anything.

Depending on the ticket, this may include reviewing:

- Microsoft Entra user state
- Authentication logs
- Group memberships
- Administrative roles
- Microsoft 365 licensing
- Exchange mailbox state
- Teams membership or policy
- SharePoint permissions
- OneDrive access
- Conditional Access
- Device identity
- Microsoft 365 Service Health
- Microsoft Entra audit logs
- Source of authority
- Microsoft Entra Connect synchronization health

The investigation should be guided by the symptom rather than by assumptions.

---

## 5. Remediate

Remediation should address the identified cause using the least disruptive and least privileged method available.

Examples include:

```text
Disabled account
        ↓
Authorized re-enable

Missing approved group membership
        ↓
Restore group membership

Missing license
        ↓
Assign required license

Incorrect synchronized attribute
        ↓
Correct authoritative on-premises value
        ↓
Synchronize

Duplicate hybrid identity
        ↓
Investigate matching conflict
        ↓
Preserve intended identity
        ↓
Remove only unintended object
```

Remediation should avoid unrelated changes.

---

## 6. Validate

An administrative action is not complete until the result is verified.

Validation may include:

- Successful user authentication
- Correct Microsoft 365 access
- Correct group membership
- Correct resource access
- Correct mailbox state
- Correct Teams policy
- Correct SharePoint permissions
- Correct device state
- Correct synchronized attributes
- Healthy synchronization service
- Correct role assignment
- Absence of unintended duplicate objects

A successful administrative click does not automatically prove that the user's issue is resolved.

---

## 7. Document

A professional support ticket should record enough information for another technician to understand what occurred.

The documentation model used in this project was:

```text
Issue / Request
      ↓
Requester / Authorization
      ↓
Impact / Scope
      ↓
Investigation
      ↓
Findings / Root Cause
      ↓
Actions Taken
      ↓
Validation
      ↓
Resolution or Escalation
```

Ticket notes should be factual and concise.

---

# Joiner Workflow

## 8. Joiner Scenario

A **Joiner** is a new employee entering the organization.

A proper onboarding workflow should begin with an approved request rather than immediately creating an account.

The capstone workflow was:

```text
Review request
      ↓
Assign / acknowledge ticket
      ↓
Verify requester and approval
      ↓
Confirm required role and access
      ↓
Provision identity
      ↓
Configure attributes
      ↓
Assign approved groups
      ↓
Assign required license
      ↓
Validate required services
      ↓
Apply security requirements
      ↓
Validate end-user access
      ↓
Document
      ↓
Close or escalate
```

---

## 9. Joiner Identity Provisioning

The new employee identity should contain accurate business information such as:

- Name
- User Principal Name
- Department
- Job title
- Company
- Usage location
- Employee type where applicable

The objective is not simply to create an account.

The identity should accurately represent the employee's organizational role.

---

## 10. Joiner Access Assignment

Access should be based on the approved role.

A technician should not blindly copy all permissions from another employee.

A better model is:

```text
Approved Job Role
      ↓
Required Department
      ↓
Approved Groups
      ↓
Required Applications / Resources
```

This helps prevent unnecessary or inherited access.

---

## 11. Joiner Licensing

The technician should assign only the Microsoft 365 services required for the employee's responsibilities.

The workflow should include validation:

```text
Identity
   ↓
License
   ↓
Service Provisioning
   ↓
End-User Access
```

A license being assigned does not automatically prove that all services are ready.

---

## 12. Joiner Security

Onboarding may also require:

- Password-change workflow
- MFA registration
- Appropriate Conditional Access
- Least-privilege access
- Approved administrative role only if required

Normal employees should not receive administrative privileges without a business requirement.

---

## 13. Joiner Validation

Before closing the ticket, validate expected access.

Examples:

```text
Can user authenticate?
Can user access required Microsoft 365 services?
Can user access approved Team / SharePoint resources?
Are required group memberships correct?
Are unnecessary privileges absent?
```

---

# Mover Workflow

## 14. Mover Scenario

A **Mover** is an employee whose organizational role changes.

Examples include:

- Department transfer
- Promotion
- Job-function change
- Temporary assignment
- Responsibility change

The lab used Joseph Daniel conceptually as the Sales-to-Finance transfer example.

---

## 15. Mover Workflow

The workflow was:

```text
Verify approved role change
        ↓
Confirm effective date
        ↓
Review current identity and access
        ↓
Update authoritative attributes
        ↓
Grant approved new access
        ↓
Remove obsolete access
        ↓
Review licensing
        ↓
Validate
        ↓
Document
```

A role change is an access-review event.

---

## 16. Privilege Creep

**Privilege creep** occurs when an employee accumulates access over time that is no longer required.

Example:

```text
Employee works in Sales
      ↓
Receives Sales access
      ↓
Moves to Finance
      ↓
Receives Finance access
      ↓
Old Sales access never removed
```

The final result is:

```text
Sales Access
+
Finance Access
```

even though the employee may only require Finance access.

Mover workflows should therefore review what should be removed, not only what should be added.

---

## 17. Source of Authority During a Mover

For synchronized users, business attributes should be changed in the appropriate authoritative system.

Example:

```text
Synchronized Job Title
        ↓
On-Premises Active Directory
        ↓
Microsoft Entra Connect
        ↓
Microsoft Entra ID
```

A technician should determine whether the attribute is:

```text
Cloud-managed
```

or:

```text
On-premises mastered
```

before making the change.

---

## 18. Mover Access Review

The technician should review:

- Existing groups
- New required groups
- Obsolete groups
- Administrative roles
- Microsoft 365 license
- Team memberships
- SharePoint permissions
- Application access

The objective is:

```text
Required access retained
New access granted
Obsolete access removed
Unnecessary privilege avoided
```

---

# Leaver Workflow

## 19. Leaver Scenario

A **Leaver** is an employee whose access must be removed because they are leaving the organization.

Offboarding is security-sensitive because timing and authorization matter.

The technician should verify:

- Authorized request
- Correct employee
- Effective termination time
- Data-preservation requirements
- Manager or business-owner requirements
- License and resource ownership considerations

---

## 20. Leaver Workflow

The capstone workflow was:

```text
Verify authorized request
        ↓
Confirm effective time
        ↓
Identify identities and access
        ↓
Disable / block sign-in
        ↓
Revoke active sessions
        ↓
Remove privileged / unnecessary access
        ↓
Preserve or transfer business data
        ↓
Review mailbox / OneDrive
        ↓
Reclaim licenses when appropriate
        ↓
Manage authoritative AD identity
        ↓
Validate access is blocked
        ↓
Document
```

---

## 21. Disable First — Do Not Immediately Delete

A key principle was:

> Disable first; do not immediately delete.

Immediate deletion may create unnecessary risk if the organization still requires:

- Email
- OneDrive data
- Audit history
- Business files
- Manager access
- Legal or retention processing
- Investigation evidence

A safer model is:

```text
Disable / Block Access
        ↓
Preserve Required Data
        ↓
Complete Business Process
        ↓
Delete Later According to Policy
```

---

## 22. Session Revocation

Disabling an identity and revoking active sessions are related but separate controls.

A leaver workflow may include:

```text
Block future sign-in
        +
Invalidate existing authentication sessions
```

This reduces the chance that an existing authenticated session remains usable after access should have ended.

---

## 23. Privileged Access Removal

Administrative access should receive special attention during offboarding.

Examples include:

- Microsoft Entra administrative roles
- Help Desk privileges
- Sensitive security groups
- Application administration
- Resource ownership

Privileged access should not remain simply because the general account was disabled.

---

## 24. Business Data Preservation

Business data may need to remain available after the employee leaves.

Examples include:

- Exchange mailbox data
- OneDrive files
- SharePoint content
- Team-owned information

The OneDrive administrative-access work from Phase 7 demonstrated how authorized administrators can access required business files without using the employee's password.

---

# Mixed Troubleshooting Capstone

## 25. Sign-In Problem Workflow

For a Microsoft 365 sign-in issue:

```text
Identify user and error
      ↓
Determine scope
      ↓
Check account state
      ↓
Review sign-in logs
      ↓
Review authentication methods / MFA
      ↓
Review Conditional Access
      ↓
Apply authorized remediation
      ↓
Validate successful authentication
      ↓
Document
```

The David Miller `50057` scenario demonstrated why account state and logs should be reviewed before automatically resetting a password.

---

## 26. Microsoft 365 Service Problem Workflow

For a Microsoft 365 application issue:

```text
Determine affected service
      ↓
Check identity and account state
      ↓
Check Microsoft 365 license
      ↓
Check required service plan
      ↓
Check provisioning
      ↓
Check permissions
      ↓
Check Microsoft 365 Service Health
      ↓
Check application / session state
      ↓
Remediate or escalate
      ↓
Validate
```

The Elena Outlook scenario demonstrated that successful authentication does not guarantee a mailbox or service entitlement.

---

## 27. Access Problem Workflow

For a resource-access issue:

```text
Correct identity?
      ↓
Correct resource?
      ↓
Required group membership?
      ↓
Group assigned to resource?
      ↓
Correct effective permission?
      ↓
Policy issue?
      ↓
Session / propagation issue?
      ↓
Validate
```

The Finance SharePoint scenario demonstrated this sequence.

---

## 28. Hybrid Attribute Problem Workflow

For an incorrect synchronized user attribute:

```text
Is user synchronized?
      ↓
Which system is authoritative?
      ↓
Check authoritative value
      ↓
Correct source value
      ↓
Run / wait for synchronization
      ↓
Validate Microsoft Entra result
```

This avoids repeatedly editing a cloud property that is mastered from on-premises Active Directory.

---

## 29. Duplicate Hybrid Identity Workflow

If two identities appear for the same employee:

```text
Do not blindly delete
        ↓
Identify both objects
        ↓
Determine legitimate identity
        ↓
Check UPN and matching
        ↓
Check synchronization scope
        ↓
Check privileged-role conflict
        ↓
Correct matching condition
        ↓
Remove only unintended object
        ↓
Synchronize
        ↓
Validate one intended identity
        ↓
Restore required access
```

The Pauline Hudson scenario demonstrated this workflow.

---

# Ticket Documentation

## 30. Ticket Structure

A useful enterprise ticket structure is:

```text
Issue / Request:
What was reported or requested?

Requester / Authorization:
Who requested it and was the change approved?

Impact / Scope:
Who or what is affected?

Investigation:
What systems, logs, configuration, or account state were checked?

Findings / Root Cause:
What actually caused the issue?

Actions:
What approved changes were performed?

Validation:
How was the result confirmed?

Resolution:
Was the issue resolved?

Escalation:
If unresolved, what evidence was provided?
```

---

## 31. Example Ticket — Authentication

```text
Issue:
User unable to access Outlook.

Investigation:
Reviewed Microsoft Entra user state and sign-in logs.

Finding:
Sign-in event recorded error 50057 indicating the user account was disabled.

Action:
Confirmed authorization and restored the intended account state.

Validation:
User authentication was retested successfully.

Resolution:
Authentication restored.
```

The exact production ticket wording would depend on the organization's procedures.

---

## 32. Example Ticket — Authorization

```text
Issue:
Finance user unable to access Finance SharePoint site.

Investigation:
Confirmed successful authentication.
Reviewed SG-Finance-Users membership and effective SharePoint permissions.

Finding:
User was missing the approved Finance security-group membership.

Action:
Restored SG-Finance-Users membership.

Validation:
Backend access was restored.
Remaining stale browser state was resolved by clearing SharePoint site cookies.

Resolution:
Finance site access restored.
```

---

## 33. Example Ticket — Hybrid Identity

```text
Issue:
Duplicate Microsoft Entra identity appeared for Pauline Hudson during synchronization.

Investigation:
Compared original cloud identity and synchronized duplicate.
Reviewed synchronization scope and existing administrative role.

Finding:
Original cloud identity held Helpdesk Administrator, creating a privileged identity-matching conflict.

Action:
Temporarily removed the cloud role and pilot synchronization scope.
Removed only the unintended duplicate after verification.
Reintroduced the intended on-premises identity to synchronization.

Validation:
Original phudson identity synchronized successfully.
No active phudson1975 duplicate remained.
Helpdesk Administrator was restored to the intended synchronized identity.

Resolution:
Single synchronized employee identity restored with required cloud role.
```

---

# Escalation

## 34. When to Escalate

A ticket should be escalated when:

- Required permissions exceed the technician's role
- The issue requires a specialized team
- The root cause remains unclear after reasonable troubleshooting
- A Microsoft-side problem requires vendor support
- Security implications require investigation
- The issue affects many users or critical services
- The change requires approval beyond Help Desk authority

Escalation is not failure.

A high-quality escalation reduces repeated work.

---

## 35. Escalation Package

A useful escalation should include:

```text
User / Device / Service
        ↓
Symptoms
        ↓
Scope / Impact
        ↓
Exact errors
        ↓
Relevant logs
        ↓
Configuration checked
        ↓
Troubleshooting already performed
        ↓
Results
        ↓
Why higher access or expertise is required
```

Avoid escalation notes such as:

```text
"Not working. Please check."
```

because they provide little value to the receiving team.

---

# Final Environment Validation

## 36. Microsoft Entra User Validation

The final hybrid identity state was reviewed.

The intended synchronized employee population was:

```text
David Miller
Elena Rivera
Joseph Daniel
Pauline Hudson
```

The final Microsoft Entra state showed:

```text
On-premises sync enabled:
Yes
```

for the four intended employee identities.

---

## 37. Duplicate Identity Validation

The Pauline remediation was reviewed to ensure that the unintended duplicate was no longer active.

Final intended identity:

```text
phudson@abhinaylabs.onmicrosoft.com
```

Unintended duplicate:

```text
phudson1975@abhinaylabs.onmicrosoft.com
```

Final validation confirmed that the unintended duplicate was not retained as an active employee identity.

---

## 38. Administrative Role Validation

Pauline Hudson's final intended synchronized identity retained the required:

```text
Helpdesk Administrator
```

Microsoft Entra role.

She was not converted into a Global Administrator for routine support work.

This preserved the least-privilege design used throughout the project.

---

## 39. Synchronization Health Validation

Microsoft Entra Connect health was validated on `SYNC01`.

The synchronization scheduler was checked using:

```powershell
Get-ADSyncScheduler |
Select-Object SyncCycleEnabled,
              StagingModeEnabled,
              SchedulerSuspended,
              SyncCycleInProgress,
              CurrentlyEffectiveSyncCycleInterval
```

The intended operational state was:

```text
SyncCycleEnabled                    : True
StagingModeEnabled                  : False
SchedulerSuspended                  : False
SyncCycleInProgress                 : False
CurrentlyEffectiveSyncCycleInterval : 00:30:00
```

---

## 40. ADSync Service Validation

The Microsoft Entra Connect service was checked using:

```powershell
Get-Service ADSync |
Select-Object Name,Status,StartType
```

The intended state was:

```text
Name      : ADSync
Status    : Running
StartType : Automatic
```

The final environment passed the synchronization health validation.

---

## 41. Device Identity Validation

The project intentionally retained two different endpoint identity models.

### CLIENT01

```text
Traditional Active Directory domain joined
Domain:
abhinaylabs.internal
```

CLIENT01 was **not** converted to Hybrid Microsoft Entra joined.

### CLOUDCLIENT01

```text
Microsoft Entra joined
AzureAdJoined : YES
DomainJoined : NO
```

This preserved a clear distinction between traditional on-premises and cloud-first endpoint identity.

---

## 42. Conditional Access Validation

The Finance Conditional Access policy remained:

```text
Report-only
```

The project demonstrated safe evaluation rather than claiming production enforcement.

This distinction was preserved during final review.

---

## 43. Synchronization Scope Validation

The final synchronization scope remained controlled.

Synchronized:

```text
David Miller
Elena Rivera
Joseph Daniel
Pauline Hudson
```

Not intentionally synchronized:

```text
Entire Active Directory
On-premises AD groups
CLIENT01
Other computer objects
```

The Microsoft Entra departmental security groups remained cloud-managed.

---

## 44. Source-of-Authority Validation

The project verified that synchronized business attributes should be updated at the authoritative source.

Example:

```text
On-Premises Active Directory
        ↓
Job Title / Department / Company
        ↓
Microsoft Entra Connect
        ↓
Microsoft Entra ID
```

Cloud-specific properties such as Microsoft Entra administrative roles remained cloud-managed.

Therefore:

```text
Hybrid identity
        =
Combination of synchronized and cloud-managed properties
```

---

## 45. Security Validation

The final security review confirmed that the project intentionally avoided publishing or relying on:

- Real employee identities
- Real organizational business data
- Passwords
- Temporary passwords
- MFA QR codes or secrets
- Recovery information
- Authentication tokens
- Personal contact information
- Billing information
- Unnecessary privileged access

All employee identities and business scenarios were synthetic.

---

## 46. Final Environment Summary

The completed technical environment included:

```text
ON-PREMISES
-----------
DC01
DC02
Active Directory Domain Services
DNS
abhinaylabs.internal

SYNC01
Microsoft Entra Connect Sync
Password Hash Synchronization

CLIENT01
Traditional AD domain-joined workstation


MICROSOFT CLOUD
---------------
Microsoft 365 Business Premium
Microsoft Entra ID P1
Exchange Online
Microsoft Teams
SharePoint Online
OneDrive
Conditional Access
Sign-In Logs
Audit Logs
Microsoft Graph PowerShell


CLOUD-FIRST ENDPOINT
--------------------
CLOUDCLIENT01
Microsoft Entra joined
```

---

## 47. Final Identity Model

The project evolved through three identity stages.

### Stage 1 — On-Premises

```text
Active Directory
      ↓
Traditional domain identities
```

### Stage 2 — Cloud

```text
Microsoft Entra ID
      ↓
Cloud-created employee identities
```

### Stage 3 — Controlled Hybrid

```text
On-Premises Active Directory
        ↓
Microsoft Entra Connect
        ↓
Existing Microsoft Entra identities
        ↓
Microsoft 365
```

This progression made it possible to understand each identity model independently before combining them.

---

## 48. Enterprise Support Principles Reinforced

The capstone reinforced several principles:

1. Verify authorization before making identity or access changes.
2. Investigate the actual problem layer before applying remediation.
3. Do not automatically reset passwords for every sign-in issue.
4. Authentication and authorization are separate concepts.
5. Licensing and service provisioning are separate from identity existence.
6. Use group-based access where appropriate instead of unnecessary direct permissions.
7. Follow least privilege for administrative roles.
8. Validate administrative changes from the user perspective.
9. Check Service Health when symptoms suggest a Microsoft-side issue.
10. Determine source of authority before modifying synchronized attributes.
11. Do not blindly delete duplicate hybrid identities.
12. Review old access during employee role changes to prevent privilege creep.
13. Disable access before immediate deletion during offboarding.
14. Preserve business data according to organizational requirements.
15. Provide useful evidence when escalating a ticket.
16. Document investigation, remediation, and validation.

---

## 49. Interview Explanation

A concise interview explanation for the capstone is:

> I completed the project by applying the Microsoft 365 and Entra skills to enterprise Help Desk workflows. For onboarding, I followed a request-and-approval model before provisioning the identity, organizational attributes, approved group access, licensing and required services, and then validated the user's access. For employee transfers, I treated the change as an access review by updating authoritative attributes, granting new role-based access and removing obsolete permissions to prevent privilege creep. For offboarding, I followed a disable-first approach, including blocking sign-in, revoking sessions, removing privileged access, preserving business data where required and reclaiming licensing according to policy rather than immediately deleting the identity. I also built troubleshooting workflows for sign-in, Microsoft 365 service, authorization and hybrid identity problems and practiced documenting root cause, remediation and validation. Finally, I validated the four-user hybrid synchronization scope, Entra Connect health, Pauline Hudson's duplicate-identity remediation, least-privilege role restoration, and the separation between the traditional CLIENT01 workstation and the Microsoft Entra joined CLOUDCLIENT01 endpoint.

---

## 50. Evidence Strategy

This capstone does not duplicate the screenshots already documented in the implementation phases.

Technical evidence is maintained in the phase where it was generated:

```text
Phase 3
Cloud Users
Screenshots 01–02

Phase 4
Groups
Screenshots 03–04

Phase 5
Licensing and Provisioning
Screenshots 05–07

Phase 6
Support and Troubleshooting
Screenshots 08–12

Phase 7
Teams / SharePoint / OneDrive
Screenshots 13–15

Phase 8
Conditional Access / Device Identity
Screenshots 16–17

Phase 9
Monitoring / PowerShell / Hybrid Identity
Screenshots 18–24
```

Phase 10 consolidates the workflows and final validation rather than reproducing the same evidence.

---

## 51. Key Lessons Learned

1. Enterprise IT Support begins with authorization and verification, not with technical changes.
2. Joiner workflows should provision access according to approved job requirements rather than blindly copying another employee.
3. Mover workflows are access-review events and should remove obsolete access to prevent privilege creep.
4. Leaver workflows should block access at the authorized time while preserving required organizational data.
5. Disable-first is generally safer than immediately deleting an employee identity.
6. Active sessions and future sign-in are separate considerations during offboarding.
7. Microsoft 365 troubleshooting should separate identity, authentication, authorization, licensing, provisioning, policy, client state and service health.
8. Hybrid identity troubleshooting requires identifying the authoritative system before making changes.
9. Duplicate identities should be investigated before deletion.
10. High-quality ticket documentation records the issue, investigation, root cause, action and validation.
11. Good escalation includes evidence and troubleshooting already completed.
12. Least privilege should apply to both on-premises and cloud administration.
13. Final validation should confirm the intended environment rather than assuming configuration changes succeeded.
14. Project scope should be described accurately; this lab synchronized four users, not the complete Active Directory environment.
15. CLIENT01 remained traditionally AD domain joined, while CLOUDCLIENT01 remained separately Microsoft Entra joined.
16. The strongest support workflow from the project is:

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
Close or Escalate
```

---

## 52. Phase Result

Phase 10 successfully brought the individual technical components of the project together into an enterprise IT Support workflow.

The capstone demonstrated:

- Joiner administration
- Mover administration
- Leaver administration
- Access review
- Privilege-creep prevention
- Disable-first offboarding
- Session-revocation awareness
- Business-data preservation
- Microsoft 365 troubleshooting methodology
- Authentication troubleshooting
- Authorization troubleshooting
- Licensing and service troubleshooting
- Hybrid identity troubleshooting
- Duplicate-identity troubleshooting
- Ticket documentation
- Escalation methodology
- Final synchronized-user validation
- Microsoft Entra Connect health validation
- Least-privilege role validation
- Device-identity boundary validation
- Conditional Access scope validation
- Final synchronization-scope validation
- Final security and privacy review

The technical implementation and validation portion of Project 2 was successfully completed.

**Phase 10 Status: COMPLETE**
