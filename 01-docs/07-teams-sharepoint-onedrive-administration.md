# Phase 7 — Microsoft Teams, SharePoint & OneDrive Administration

## 1. Objective

The objective of this phase was to practice administration and support across three closely related Microsoft 365 collaboration services:

- Microsoft Teams
- SharePoint Online
- OneDrive

The phase focused on:

- Creating and administering a Microsoft Team
- Managing Team owners and members
- Creating a standard channel
- Testing membership-based access
- Creating and assigning a Teams messaging policy
- Validating policy behavior
- Understanding the relationship between Teams and SharePoint
- Reviewing SharePoint site configuration
- Reviewing external-sharing settings
- Reviewing OneDrive administration
- Performing authorized administrative access to a user's OneDrive
- Understanding business-continuity and offboarding considerations

---

## 2. Microsoft Teams

Microsoft Teams is a Microsoft 365 collaboration service used for:

- Chat
- Meetings
- Team collaboration
- Channels
- File sharing
- Microsoft 365 application integration

Teams does not operate as a completely isolated service.

It integrates with other Microsoft 365 services, especially:

- Microsoft Entra ID
- SharePoint Online
- OneDrive
- Exchange Online

Understanding these relationships is important when troubleshooting Teams access or file issues.

---

## 3. Finance Team

A private Microsoft Team was created for the fictional Finance department.

The Team represented a departmental collaboration workspace.

The lab configuration included:

```text
Team:
Finance

Privacy:
Private
```

Using a private Team meant that membership was controlled rather than allowing unrestricted organizational access.

---

## 4. Team Ownership

Elena Rivera was configured as an owner of the Finance Team.

Conceptually:

```text
Finance Team
     |
     +-- Elena Rivera
             |
             +-- Owner
```

A Team owner has additional management capabilities compared with a normal Team member.

Typical owner responsibilities may include:

- Managing membership
- Managing selected Team settings
- Organizing collaboration
- Supporting departmental administration

This differs from a standard member, whose primary responsibility is collaboration within the Team.

---

## 5. Owner vs Member

The difference between Team owners and members is important.

### Owner

An owner can manage the Team and supported membership/settings.

### Member

A member participates in collaboration and accesses resources made available to Team members.

Conceptually:

```text
Owner
  ↓
Manage Team + Collaborate

Member
  ↓
Collaborate
```

The lab used this distinction to create a realistic departmental collaboration model.

---

## 6. Standard Channel

A standard channel named:

```text
Budget and Reporting
```

was created inside the Finance Team.

The structure became:

```text
Finance Team
     |
     +-- Budget and Reporting
             |
             +-- Standard Channel
```

A standard channel is available to members of the parent Team.

This became useful when validating how Team membership affected access to channel content.

---

## 7. Membership-Based Access Test

David Miller was temporarily added to the Finance Team to test membership-based access.

The workflow was:

```text
David not in Finance Team
        ↓
Add David as Team member
        ↓
Validate access
        ↓
Remove David
        ↓
Validate access removal
```

This demonstrated that Team membership directly affects access to the Team's standard collaboration resources.

The test was performed only with synthetic identities in the lab.

---

## 8. Membership Lifecycle

The Team membership test represented a simple access lifecycle.

```text
Grant
  ↓
Validate
  ↓
Revoke
  ↓
Validate
```

This is an important administrative pattern.

An access change is not complete merely because an administrator clicked **Add** or **Remove**.

The resulting user experience should also be validated.

---

## 9. Microsoft Teams Policies

Microsoft Teams policies control supported Teams features available to users.

Examples may include configuration for:

- Messaging
- Meetings
- Calling
- Applications
- Other Teams functionality

The lab focused on a custom messaging policy.

---

## 10. Finance Messaging Policy

A custom Teams messaging policy was created:

```text
Finance-Messaging-Policy
```

The policy was directly assigned to Elena Rivera for controlled testing.

The administrative path was:

```text
Custom Teams policy
        ↓
Assign to Elena Rivera
        ↓
Validate user behavior
```

This demonstrated that Teams behavior can be influenced by administrative policy rather than only by the local Teams application.

---

## 11. Message Editing Test

The custom policy was used to test message-editing behavior.

During the controlled test:

```text
Edit sent messages
        ↓
Disabled
```

The effect was validated from the user perspective.

After testing, Elena was returned to the appropriate standard policy state.

This demonstrated the full configuration lifecycle:

```text
Configure
   ↓
Assign
   ↓
Validate
   ↓
Restore
   ↓
Validate
```

---

## 12. Teams Policy Troubleshooting Principle

A feature-specific Teams problem should not automatically lead to application reinstallation.

For example:

```text
User says:
"I cannot edit a sent Teams message."
```

A useful investigation path is:

```text
Correct user?
      ↓
Microsoft 365 license?
      ↓
Team membership?
      ↓
Assigned Teams policy?
      ↓
Policy configuration?
      ↓
Client / service state?
```

If a policy intentionally disables a feature, reinstalling Teams would not solve the underlying cause.

---

## 13. Teams and SharePoint Integration

A major concept demonstrated in this phase was the relationship between Microsoft Teams and SharePoint Online.

Files uploaded to standard Teams channels are stored in the Team's associated SharePoint document library.

Conceptually:

```text
Microsoft Teams
      |
      +-- Finance Team
             |
             +-- Budget and Reporting
                     |
                     +-- Channel File
                              |
                              v
                     SharePoint Online
```

This means a file visible in Teams may actually be stored and governed through SharePoint.

---

## 14. File Integration Test

The lab used a Finance document named:

```text
September Budget Notes.docx
```

The file was accessed through the Finance Team's:

```text
Budget and Reporting
```

channel.

The same content was then verified through the corresponding SharePoint location.

This demonstrated that the standard Teams channel and SharePoint document library were connected.

---

## 15. Why the Teams and SharePoint Relationship Matters

Understanding the Teams-to-SharePoint relationship helps prevent incorrect troubleshooting.

A user may report:

```text
"My Teams file is missing."

"I cannot open a file from Teams."

"I lost access to a channel document."
```

The actual issue may involve:

- Team membership
- SharePoint permissions
- SharePoint site configuration
- File permissions
- Microsoft 365 licensing
- Client/session state

Therefore:

```text
Teams file issue
        ≠
Always a Teams application issue
```

The technician should investigate the underlying Microsoft 365 service relationship.

---

## 16. SharePoint Administration

The SharePoint Admin Center was used to review the SharePoint environment.

Administrative areas reviewed included:

- Active sites
- Site storage
- Sharing configuration
- Microsoft Teams-associated SharePoint resources

This reinforced that SharePoint is an important backend service for Microsoft 365 collaboration.

---

## 17. SharePoint Storage

SharePoint sites consume organizational cloud storage.

The lab reviewed storage settings for the Microsoft 365 environment.

SharePoint storage can be administered using tenant-level storage management and, depending on configuration, individual site quotas.

The important support concept was:

```text
Team collaboration files
        ↓
SharePoint storage
```

Storage issues can therefore affect collaboration services that users may primarily experience through Teams.

---

## 18. SharePoint External Sharing

External-sharing configuration was reviewed for the Finance collaboration environment.

External sharing determines whether organizational content may be shared outside the tenant and under what conditions.

A general security principle is:

> Use the least permissive sharing configuration that still satisfies the legitimate business requirement.

More permissive sharing can improve collaboration but also increases potential data-exposure risk.

---

## 19. OneDrive

OneDrive is Microsoft 365 storage primarily designed for an individual user's work files.

A useful distinction is:

```text
OneDrive
   ↓
Individual work files

SharePoint / Teams
   ↓
Organizational and team collaboration
```

This distinction matters during administration, troubleshooting, employee transfers, and offboarding.

---

## 20. OneDrive Administration

The Microsoft 365 / SharePoint administration experience was used to review OneDrive-related settings.

The lab included review of:

- User OneDrive storage
- Sharing
- Retention-related configuration
- Administrative access

This provided practical exposure to the types of OneDrive administration commonly needed during support and employee lifecycle events.

---

## 21. Authorized OneDrive Administrative Access

A controlled business-continuity scenario was performed using David Miller's OneDrive.

The administrator obtained authorized access to David's OneDrive without using David's password.

The workflow was:

```text
Administrator
      ↓
Authorized administrative access
      ↓
David Miller's OneDrive
      ↓
Business file
```

The test file was:

```text
HR-Handover-Notes.docx
```

This demonstrated that legitimate administrative access should use supported administrative mechanisms rather than asking for or using the employee's credentials.

---

## 22. Why Administrative File Access Matters

Organizations may need access to an employee's business files for legitimate reasons such as:

- Employee absence
- Offboarding
- Business continuity
- Manager-requested file transfer
- Authorized investigation
- Data preservation

A proper administrative workflow should be authorized and documented.

It should not require obtaining the user's password.

---

## 23. OneDrive Retention

The lab reviewed the configured OneDrive retention behavior.

The observed lab setting was:

```text
30 days
```

The purpose of retention is to provide a period during which former-user OneDrive data can be handled or recovered according to configured Microsoft 365 behavior and organizational policy.

This is especially important during employee offboarding.

---

## 24. OneDrive External Sharing

The lab also reviewed OneDrive external-sharing configuration.

David's OneDrive environment permitted sharing options that included external collaboration.

This demonstrated the trade-off between:

```text
Collaboration flexibility
        vs
Data exposure risk
```

A production organization should configure sharing according to its security and business requirements.

The project did not treat the permissive lab setting as a universal recommended production configuration.

---

## 25. Teams vs SharePoint vs OneDrive

The three services serve related but different purposes.

| Service           | Primary Purpose                               |
| ----------------- | --------------------------------------------- |
| Microsoft Teams   | Communication and team collaboration          |
| SharePoint Online | Organizational/team content and collaboration |
| OneDrive          | Individual user's work files                  |

The services are integrated.

For example:

```text
Teams Standard Channel
        ↓
SharePoint Document Library
```

while:

```text
Individual employee files
        ↓
OneDrive
```

Understanding these relationships helps support technicians troubleshoot the correct backend service.

---

## 26. Access Troubleshooting Model

When a user reports a collaboration-access problem, a useful sequence is:

```text
Correct user?
      ↓
Account enabled?
      ↓
Correct Microsoft 365 license?
      ↓
Correct Team membership?
      ↓
Correct Teams policy?
      ↓
Correct SharePoint permissions?
      ↓
Sharing configuration?
      ↓
Client / session state?
      ↓
Microsoft Service Health?
```

The exact sequence depends on the reported symptom, but the technician should avoid immediately reinstalling an application or creating direct permissions.

---

## 27. Example — Teams Feature Issue

Reported issue:

```text
"I cannot edit my Teams message."
```

Investigation:

```text
Identity valid?
      ↓
License present?
      ↓
Teams accessible?
      ↓
Assigned messaging policy?
      ↓
Edit-message setting disabled?
```

If policy is the cause:

```text
Policy configuration
        =
Root cause
```

not:

```text
Broken Teams installation
```

---

## 28. Example — Teams File Issue

Reported issue:

```text
"I cannot access a file from the Finance Team."
```

Possible investigation:

```text
Team membership
      ↓
Channel access
      ↓
Underlying SharePoint site
      ↓
SharePoint permission
      ↓
File availability
      ↓
Client/session state
```

This avoids treating Teams as an isolated application.

---

## 29. Example — OneDrive Business Continuity

Scenario:

```text
Employee unavailable
      ↓
Authorized business file required
      ↓
Administrator receives approval
      ↓
Use supported OneDrive administrative access
      ↓
Retrieve required business data
      ↓
Document action
```

The user password should not be requested simply to access organizational data through an approved administrative workflow.

---

## 30. Enterprise Relevance

Microsoft Teams, SharePoint, and OneDrive are common components of modern enterprise collaboration environments.

IT Support teams regularly receive tickets involving:

```text
"User cannot access a Team."

"User needs to be added to a department Team."

"Teams policy is blocking a feature."

"Channel file is missing."

"User cannot access SharePoint."

"Former employee's OneDrive files are required."

"External sharing needs to be reviewed."
```

Supporting these services requires understanding both the visible application and the underlying Microsoft 365 architecture.

---

## 31. IT Support Relevance

This phase practiced several common IT Support responsibilities:

- Team creation
- Owner administration
- Membership administration
- Access validation
- Teams policy administration
- Policy troubleshooting
- SharePoint administration
- SharePoint storage review
- External-sharing review
- Teams-to-SharePoint file troubleshooting
- OneDrive administration
- Administrative access to business files
- Retention awareness
- Business-continuity support

These tasks are directly relevant to Service Desk and Microsoft 365 support roles.

---

## 32. Security and IAM Relevance

The phase also demonstrated several security concepts.

### Least Privilege

Access should be granted only to users who require it.

### Membership Lifecycle

Access should be validated when users are added or removed.

### External Sharing

External collaboration should follow organizational security policy.

### Administrative Access

Administrative access to employee files should be authorized and auditable.

### Data Preservation

Employee business data may need to be retained or transferred during offboarding.

### Credential Protection

Administrators should use supported administrative mechanisms rather than using employee passwords.

---

## 33. Evidence

### Figure 13 — Teams Messaging Policy Assignment

The custom `Finance-Messaging-Policy` was assigned to Elena Rivera and validated from the user's Teams experience.

![Teams Messaging Policy Assignment](../02-screenshots/13-teams-messaging-policy-assignment.png)

### Figure 14 — Teams and SharePoint File Integration

The Finance document was verified through both the Teams standard channel and its corresponding SharePoint-backed storage location.

![Teams and SharePoint File Integration](../02-screenshots/14-teams-sharepoint-file-integration.png)

### Figure 15 — OneDrive Administrative File Access

Authorized administrative access to David Miller's OneDrive demonstrated a business-continuity workflow without using the employee's password.

![OneDrive Administrative File Access](../02-screenshots/15-onedrive-administrative-file-access.png)

---

## 34. Interview Explanation

A concise interview explanation for this phase is:

> In my Microsoft 365 lab, I created and administered a private departmental Team, configured Elena Rivera as an owner, created a standard Budget and Reporting channel, and tested the full grant-and-revoke membership lifecycle with another synthetic user. I also created and directly assigned a custom Teams messaging policy, changed message-editing behavior, validated the effect from the user's perspective, and then restored the appropriate policy state. I demonstrated that files in standard Teams channels are backed by SharePoint and reviewed SharePoint storage and external-sharing controls. For OneDrive, I reviewed administrative storage, sharing and retention settings and used Microsoft's supported administrative-access workflow to access a user's business file for a simulated business-continuity scenario without using the user's credentials.

---

## 35. Key Lessons Learned

1. Microsoft Teams is integrated with other Microsoft 365 services rather than operating independently.
2. Team owners and members have different responsibilities and capabilities.
3. Standard channels are available to members of the parent Team.
4. Membership changes should be followed by end-user validation.
5. Teams policies can control user features and should be checked before assuming the client application is broken.
6. A feature-specific Teams issue does not automatically require reinstallation.
7. Files in standard Teams channels are stored in the associated SharePoint document library.
8. A Teams file problem may actually involve SharePoint access or storage.
9. OneDrive is primarily intended for individual work files, while SharePoint and Teams support broader organizational collaboration.
10. Authorized administrators can access user OneDrive data through supported administrative mechanisms without using the user's password.
11. OneDrive retention and administrative access are important during offboarding and business-continuity scenarios.
12. External sharing increases collaboration capability but also increases potential data-exposure risk.
13. Collaboration troubleshooting should consider identity, licensing, membership, policy, permissions, client state, and service health.

---

## 36. Phase Result

Phase 7 successfully demonstrated administration and support across Microsoft Teams, SharePoint Online, and OneDrive.

The phase included:

- Private Team creation
- Team ownership configuration
- Standard-channel creation
- Membership grant and revoke testing
- End-user access validation
- Custom Teams messaging policy creation
- Direct policy assignment
- Policy behavior validation
- Teams-to-SharePoint file integration
- SharePoint site and storage review
- External-sharing review
- OneDrive administration
- Authorized OneDrive administrative access
- Business-continuity file access
- OneDrive retention awareness
- Collaboration troubleshooting methodology

The phase demonstrated how Microsoft 365 collaboration services are interconnected and why support technicians must troubleshoot the underlying service relationships rather than treating each application in isolation.

**Phase 7 Status: COMPLETE**
