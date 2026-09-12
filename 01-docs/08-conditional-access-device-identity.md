# Phase 8 — Conditional Access, Security & Microsoft Entra Device Identity

## 1. Objective

The objective of this phase was to introduce cloud access-control and device-identity concepts used in modern Microsoft environments.

The phase focused on:

- Microsoft Entra Conditional Access
- Report-only policy testing
- Safe policy evaluation
- Conditional Access sign-in evidence
- The Conditional Access What If tool
- Microsoft Entra registered devices
- Microsoft Entra joined devices
- Hybrid Microsoft Entra joined devices
- Windows device-state validation
- `dsregcmd /status`
- Primary Refresh Token concepts
- Web Account Manager concepts
- Device identity versus device management
- Cloud-first Windows endpoint administration

The goal was to understand how user identity, access policy, device identity, and authentication state interact without unnecessarily enforcing disruptive controls in the lab.

---

## 2. Conditional Access

Microsoft Entra Conditional Access is a policy engine that evaluates sign-in conditions before determining whether access controls should apply.

Conditional Access can evaluate signals such as:

- User
- Group
- Cloud application
- Device state
- Location
- Authentication context
- Risk-related signals
- Other supported conditions

Conceptually:

```text
User attempts sign-in
        ↓
Microsoft Entra evaluates conditions
        ↓
Conditional Access policy evaluated
        ↓
Access control decision
```

Conditional Access is therefore different from simply enabling MFA globally for every scenario.

It allows organizations to apply access requirements according to defined conditions.

---

## 3. Finance Conditional Access Policy

A Conditional Access policy was created for the Finance scenario.

The policy was named:

```text
CA-Require-MFA-Finance
```

The policy targeted Elena Rivera in the Finance scenario and evaluated access to Office 365 Exchange Online.

The intended access control was:

```text
Require MFA
```

However, the policy was intentionally kept in:

```text
Report-only
```

mode.

---

## 4. Report-Only Mode

Report-only mode allows administrators to evaluate how a Conditional Access policy would behave without actively enforcing the access control.

Conceptually:

```text
Policy configured
      ↓
Report-only
      ↓
Real sign-in evaluated
      ↓
Result recorded
      ↓
User access not blocked by this policy
```

This is useful because a poorly designed Conditional Access policy can accidentally disrupt legitimate access.

A safer administrative workflow is:

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
Enforce only when approved
```

The lab stopped at the safe evaluation stage.

The project does **not** claim that the Finance Conditional Access policy was placed into production-style enforcement.

---

## 5. Conditional Access Evaluation

The policy was evaluated through actual Microsoft Entra sign-in activity.

The sign-in evidence showed that the Finance Conditional Access policy was evaluated for the selected user and application scenario.

This demonstrated the relationship between:

```text
Sign-in
   ↓
Conditional Access evaluation
   ↓
Policy result
```

The policy remained in Report-only mode during the validation.

---

## 6. Conditional Access What If Tool

The Conditional Access **What If** tool was also used to simulate a sign-in scenario.

The tool allows administrators to enter conditions such as:

- User
- Cloud application
- Device information
- Location
- Other supported sign-in conditions

and determine which Conditional Access policies would apply.

Conceptually:

```text
Simulated sign-in conditions
        ↓
What If evaluation
        ↓
Applicable policies identified
```

This provides another way to evaluate policy logic before enforcement.

A dedicated What If screenshot was not required for the public portfolio because the actual Report-only evaluation already provided stronger implementation evidence.

---

## 7. Conditional Access Troubleshooting

When a Microsoft 365 user reports an access problem, Conditional Access may be one of several possible causes.

A useful troubleshooting sequence is:

```text
Correct identity?
      ↓
Account enabled?
      ↓
Authentication successful?
      ↓
Conditional Access evaluated?
      ↓
Which policy applied?
      ↓
Which control was required?
      ↓
Device state relevant?
      ↓
Application / service healthy?
```

Administrators should avoid changing or disabling Conditional Access policies without first examining the sign-in evidence.

---

## 8. Device Identity

Microsoft Entra can maintain identities for devices in addition to users and groups.

A device identity allows Microsoft Entra to recognize a device and use its state in supported identity and access scenarios.

Common Microsoft Entra device states include:

- Microsoft Entra registered
- Microsoft Entra joined
- Hybrid Microsoft Entra joined

These states are not interchangeable.

---

## 9. Microsoft Entra Registered

A **Microsoft Entra registered** device has an identity in Microsoft Entra but is not necessarily fully joined to the organization.

This state is commonly associated with:

- Personally owned devices
- BYOD scenarios
- Work accounts added to personal devices

Conceptually:

```text
Personal / BYOD device
        ↓
Work account registered
        ↓
Microsoft Entra device identity
```

A registered device is different from a Microsoft Entra joined organizational endpoint.

The project reviewed this distinction conceptually but did not publish personal-device evidence.

---

## 10. Microsoft Entra Joined

A **Microsoft Entra joined** device is joined directly to Microsoft Entra ID rather than to a traditional on-premises Active Directory domain.

Conceptually:

```text
Windows device
      ↓
Microsoft Entra ID
      ↓
Organizational cloud identity
```

This model is commonly used for cloud-first Windows environments.

---

## 11. Hybrid Microsoft Entra Joined

A **Hybrid Microsoft Entra joined** Windows device is:

```text
Joined to on-premises Active Directory
        +
Represented as a joined device in Microsoft Entra ID
```

Conceptually:

```text
On-Premises AD DS
        |
        +-- Windows device
                |
                +-- Hybrid Microsoft Entra identity
```

This differs from a pure Microsoft Entra joined device.

The project studied the distinction, but the Phase 8 endpoint was **not** configured as Hybrid Microsoft Entra joined.

---

## 12. CLOUDCLIENT01

A separate Windows 11 Enterprise virtual machine was deployed for the cloud-first device scenario.

The computer name was:

```text
CLOUDCLIENT01
```

The endpoint was intentionally kept separate from the traditional Active Directory workstation used in the on-premises lab.

The architecture became:

```text
CLIENT01
   |
   +-- Traditional AD domain joined
   |
   +-- abhinaylabs.internal


CLOUDCLIENT01
   |
   +-- Microsoft Entra joined
   |
   +-- Not domain joined
```

This allowed both traditional and cloud-first device models to exist in the same broader lab environment without converting the original workstation.

---

## 13. Microsoft Entra Join

CLOUDCLIENT01 was joined to Microsoft Entra ID using a standard organizational identity.

The resulting device appeared in the Microsoft Entra admin center as:

```text
Device:
CLOUDCLIENT01

Join Type:
Microsoft Entra joined
```

The device owner was associated with the synthetic organizational user used during the join.

This provided cloud-side confirmation of the device identity.

---

## 14. Local Device Validation

The Windows command:

```cmd
hostname
```

was used to confirm the local computer name.

Expected result:

```text
CLOUDCLIENT01
```

The primary device-identity troubleshooting command was:

```cmd
dsregcmd /status
```

This command displays Windows registration, join, tenant, and authentication information.

---

## 15. `dsregcmd /status`

The important device-state results were:

```text
AzureAdJoined : YES
EnterpriseJoined : NO
DomainJoined : NO
Device Name : CLOUDCLIENT01
```

Although Microsoft now uses the Microsoft Entra branding, the Windows command output still uses the historical:

```text
AzureAdJoined
```

terminology.

The result:

```text
AzureAdJoined : YES
```

confirmed that CLOUDCLIENT01 was Microsoft Entra joined.

The result:

```text
DomainJoined : NO
```

confirmed that it was not joined to the on-premises Active Directory domain.

---

## 16. Device State Interpretation

The device state could therefore be interpreted as:

```text
Microsoft Entra joined:
YES

Traditional Active Directory domain joined:
NO

Hybrid Microsoft Entra joined:
NO
```

This is important because the device should not be described as hybrid joined.

The correct portfolio claim is:

> CLOUDCLIENT01 was Microsoft Entra joined as a cloud-first Windows endpoint.

---

## 17. WorkplaceJoined

The tested user context showed:

```text
WorkplaceJoined : NO
```

This reinforced that CLOUDCLIENT01 was not merely operating as a workplace / Microsoft Entra registered device in that context.

Instead, the machine had the stronger device state:

```text
AzureAdJoined : YES
```

---

## 18. Primary Refresh Token

The user state showed:

```text
AzureAdPrt : YES
```

A **Primary Refresh Token**, or PRT, is an authentication artifact used by Windows to support single sign-on to Microsoft Entra-integrated applications.

Conceptually:

```text
User authenticates to Windows
        ↓
Microsoft Entra authentication state
        ↓
PRT available
        ↓
Supports SSO to Entra-backed resources
```

The presence of:

```text
AzureAdPrt : YES
```

showed that the organizational user had a PRT in the tested session.

---

## 19. Web Account Manager

The user state also showed:

```text
WamDefaultSet : YES
```

WAM stands for:

```text
Web Account Manager
```

Windows Web Account Manager acts as an authentication broker used by Windows applications when working with organizational accounts.

The value:

```text
WamDefaultSet : YES
```

showed that the organizational account was available through WAM in the tested context.

---

## 20. Device Identity vs Device Management

A major lesson from this phase was that device identity and device management are different concepts.

CLOUDCLIENT01 was:

```text
Microsoft Entra joined
```

but the device-state information showed no automatic mobile-device-management enrollment for this test.

Therefore:

```text
Microsoft Entra joined
        ≠
Automatically Intune managed
```

Microsoft Entra establishes the device identity.

Microsoft Intune is a separate endpoint-management platform.

They can work together, but one does not automatically mean the other is configured.

---

## 21. Why Intune Was Not Expanded Here

The purpose of this phase was to understand:

- Device identity
- Microsoft Entra join state
- Authentication state
- Conditional Access relationships

A full Intune endpoint-management deployment was not required to prove those concepts.

Deeper endpoint administration belongs more naturally in the separate Windows endpoint / device-management project rather than unnecessarily expanding this Microsoft 365 identity lab.

---

## 22. CLIENT01 vs CLOUDCLIENT01

The broader lab now contained two different Windows identity models.

### CLIENT01

```text
Traditional Active Directory domain joined
Domain:
abhinaylabs.internal
```

### CLOUDCLIENT01

```text
Microsoft Entra joined
AzureAdJoined : YES
DomainJoined : NO
```

This provided practical exposure to both traditional enterprise and cloud-first Windows identity.

---

## 23. Device Troubleshooting Model

When troubleshooting Microsoft Entra device identity, a useful sequence is:

```text
Confirm device name
      ↓
Run dsregcmd /status
      ↓
Check AzureAdJoined
      ↓
Check DomainJoined
      ↓
Check WorkplaceJoined
      ↓
Check PRT / user state
      ↓
Check device in Entra admin center
      ↓
Check sign-in logs
      ↓
Check Conditional Access
      ↓
Check licensing / application
```

The technician should avoid immediately disconnecting or rejoining a device without first understanding its existing state.

---

## 24. Example — Microsoft 365 Sign-In Problem on a Device

A user on a Microsoft Entra joined device may report:

```text
"I cannot access Microsoft 365."
```

A support technician may need to check:

```text
User identity
      ↓
Account state
      ↓
Device join state
      ↓
PRT state
      ↓
Sign-in logs
      ↓
Conditional Access
      ↓
License
      ↓
Microsoft service health
      ↓
Application / client state
```

This demonstrates how device identity can become another layer in Microsoft 365 troubleshooting.

---

## 25. Conditional Access and Device Identity Relationship

Conditional Access can use supported device information when evaluating access.

Conceptually:

```text
User
   +
Application
   +
Device state
   +
Other signals
        ↓
Conditional Access
        ↓
Access decision
```

Understanding device identity therefore becomes increasingly important as organizations use more advanced access policies.

---

## 26. Enterprise Relevance

Modern organizations may use different endpoint identity models depending on infrastructure and business requirements.

Examples include:

```text
Traditional environment
        ↓
Active Directory domain joined

Cloud-first environment
        ↓
Microsoft Entra joined

Hybrid environment
        ↓
Hybrid Microsoft Entra joined
```

Service Desk and endpoint-support personnel need to identify the actual device state before troubleshooting authentication or access issues.

---

## 27. IT Support Relevance

Common device-related support tickets may include:

```text
"User cannot sign into Microsoft 365 from this laptop."

"Device is not appearing in Entra."

"User has no SSO."

"Conditional Access is affecting this sign-in."

"Is this computer domain joined or Entra joined?"

"Why is the device in Entra but not Intune?"
```

Commands such as:

```cmd
hostname
dsregcmd /status
```

provide useful local evidence before making configuration changes.

---

## 28. Security and IAM Relevance

This phase connected identity, policy, and endpoint security concepts.

### Conditional Access

Evaluates contextual signals before applying access controls.

### MFA

Can be required by Conditional Access policies.

### Device Identity

Allows Microsoft Entra to identify organizational devices.

### PRT

Supports cloud authentication and SSO on Windows.

### Least Disruption

Policies should be evaluated safely before enforcement.

### Device Management Separation

A device being recognized by Microsoft Entra does not automatically mean that endpoint-management controls are deployed.

---

## 29. Evidence

### Figure 16 — Conditional Access Report-Only Evaluation

The Finance Conditional Access policy was evaluated through Microsoft Entra sign-in activity while remaining in Report-only mode.

![Conditional Access Report-Only Evaluation](../02-screenshots/16-conditional-access-report-only-evaluation.png)

### Figure 17 — Microsoft Entra Joined CLOUDCLIENT01

CLOUDCLIENT01 was validated as a Microsoft Entra joined Windows endpoint through local device-state information and the Microsoft Entra admin center.

![Microsoft Entra Joined CLOUDCLIENT01](../02-screenshots/17-microsoft-entra-joined-cloudclient01.png)

---

## 30. Commands Used

### Verify Computer Name

```cmd
hostname
```

Purpose:

```text
Displays the Windows computer name.
```

### Inspect Microsoft Entra and Domain Join State

```cmd
dsregcmd /status
```

Purpose:

```text
Displays Windows Microsoft Entra registration/join state,
domain state, tenant information, and user authentication state.
```

Important values observed on CLOUDCLIENT01:

```text
AzureAdJoined : YES
EnterpriseJoined : NO
DomainJoined : NO
Device Name : CLOUDCLIENT01
```

Additional user/session values observed:

```text
WorkplaceJoined : NO
WamDefaultSet : YES
AzureAdPrt : YES
```

---

## 31. Interview Explanation

A concise interview explanation for this phase is:

> In my Microsoft 365 and Entra lab, I created a Conditional Access policy requiring MFA for the Finance scenario and kept it in Report-only mode so I could safely evaluate its effect before enforcement. I validated the policy through Microsoft Entra sign-in evidence and also used the Conditional Access What If tool. I then deployed a separate Windows 11 Enterprise VM named CLOUDCLIENT01 and Microsoft Entra joined it using a standard organizational user. I validated the device locally with `dsregcmd /status`, which showed `AzureAdJoined: YES` and `DomainJoined: NO`, and I confirmed the device from the Entra admin center. I also reviewed PRT and WAM state for cloud authentication and learned that an Entra-joined device is not automatically Intune-managed.

---

## 32. Key Lessons Learned

1. Conditional Access evaluates sign-in conditions before applying configured access controls.
2. Report-only mode allows administrators to evaluate a policy without immediately enforcing it.
3. Conditional Access should be tested and validated before production-style enforcement.
4. Sign-in logs can show how a Conditional Access policy evaluated a real authentication attempt.
5. The What If tool can simulate policy applicability before enforcement.
6. Microsoft Entra registered, Microsoft Entra joined, and Hybrid Microsoft Entra joined are different device states.
7. `dsregcmd /status` is a key Windows command for investigating Microsoft Entra device identity.
8. `AzureAdJoined : YES` confirmed that CLOUDCLIENT01 was Microsoft Entra joined.
9. `DomainJoined : NO` confirmed that CLOUDCLIENT01 was not joined to the on-premises Active Directory domain.
10. CLOUDCLIENT01 should not be described as Hybrid Microsoft Entra joined.
11. `AzureAdPrt : YES` demonstrated the user's Primary Refresh Token state for SSO.
12. `WamDefaultSet : YES` demonstrated the presence of the organizational account through Windows Web Account Manager.
13. Microsoft Entra device identity and Intune device management are separate concepts.
14. A support technician should verify device state before unnecessarily disconnecting or rejoining a device.
15. Maintaining separate traditional and cloud-first endpoints made the differences between AD domain join and Microsoft Entra join easier to understand.

---

## 33. Phase Result

Phase 8 successfully demonstrated Microsoft Entra Conditional Access evaluation and cloud-first Windows device identity.

The phase included:

- Conditional Access concepts
- Finance MFA policy configuration
- Report-only deployment
- Real sign-in policy evaluation
- Conditional Access What If testing
- Microsoft Entra registered concepts
- Microsoft Entra joined concepts
- Hybrid Microsoft Entra joined concepts
- Windows 11 Enterprise cloud endpoint deployment
- CLOUDCLIENT01 Microsoft Entra join
- `hostname` validation
- `dsregcmd /status`
- PRT validation
- WAM validation
- Device identity versus device management
- Conditional Access and device troubleshooting methodology

The phase provided the foundation for the deeper monitoring, Microsoft Graph PowerShell, and hybrid identity work performed next.

**Phase 8 Status: COMPLETE**

