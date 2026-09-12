# Phase 2 — Microsoft Entra ID Fundamentals

## 1. Objective

The objective of this phase was to understand the core Microsoft Entra ID concepts required before performing user administration, licensing, authentication troubleshooting, role assignment, device administration, and hybrid identity configuration.

The focus was to understand how Microsoft cloud identity works and how it differs from the traditional on-premises Active Directory model used in the previous Active Directory IT Support Lab.

---

## 2. Microsoft Entra ID

**Microsoft Entra ID** is Microsoft's cloud identity and access management service.

It was previously known as:

```text
Azure Active Directory
```

Microsoft Entra ID manages identities used to access cloud services such as:

- Microsoft 365
- Exchange Online
- Microsoft Teams
- SharePoint Online
- OneDrive
- Azure
- SaaS applications
- Other applications integrated with Microsoft identity

In the Abhinay Labs environment, Microsoft Entra ID became the central cloud directory for users, groups, administrative roles, authentication, devices, security policies, and Microsoft 365 access.

---

## 3. Tenant

A **tenant** is an organization's isolated Microsoft cloud environment.

The lab tenant was:

```text
Organization: Abhinay Labs
Tenant domain: abhinaylabs.onmicrosoft.com
```

The tenant provided a separate cloud identity boundary for the fictional organization.

Conceptually:

```text
Microsoft Cloud
      |
      +-- Abhinay Labs Tenant
              |
              +-- Users
              +-- Groups
              +-- Devices
              +-- Applications
              +-- Administrative Roles
              +-- Authentication
              +-- Security Policies
```

Users and administrators within the Abhinay Labs tenant were managed separately from identities belonging to other Microsoft tenants.

---

## 4. Directory Objects

A **directory object** is an identity-related object stored in Microsoft Entra ID.

Common directory objects include:

- Users
- Groups
- Devices
- Applications
- Service principals

Examples from this lab included:

```text
User:
David Miller

Group:
SG-HR-Users

Device:
CLOUDCLIENT01
```

Each object represents something that Microsoft Entra ID can identify, manage, or use during authentication and authorization decisions.

---

## 5. User Principal Name

A **User Principal Name**, or **UPN**, is the sign-in name commonly used by a Microsoft Entra user.

A typical UPN has the format:

```text
username@domain
```

Example from the lab:

```text
dmiller@abhinaylabs.onmicrosoft.com
```

Other synthetic employee UPNs included:

```text
erivera@abhinaylabs.onmicrosoft.com
jdaniel@abhinaylabs.onmicrosoft.com
phudson@abhinaylabs.onmicrosoft.com
```

The UPN is important because it identifies the user during Microsoft 365 and Entra authentication.

Later in the project, matching UPNs also became important during controlled hybrid identity synchronization.

---

## 6. Member and Guest Users

Microsoft Entra ID supports different user types.

### Member

A **Member** normally represents an internal organizational identity.

The primary synthetic employees in the lab were configured as:

```text
User type: Member
```

Examples:

- David Miller
- Elena Rivera
- Joseph Daniel
- Pauline Hudson

### Guest

A **Guest** normally represents an external identity invited to access selected organizational resources.

A guest user may represent:

- Contractor
- Vendor
- Partner
- External consultant
- User from another organization

The lab primarily used Member identities because the scenarios focused on internal employees.

---

## 7. Authentication

**Authentication**, commonly shortened to **AuthN**, verifies who a user is.

Examples of authentication factors include:

- Password
- Microsoft Authenticator
- Passkey
- Hardware token
- Other supported authentication methods

Conceptually:

```text
User claims identity
        |
        v
Provides credential
        |
        v
Microsoft Entra ID verifies identity
        |
        v
Authentication succeeds or fails
```

Example:

```text
David Miller
        |
        v
dmiller@abhinaylabs.onmicrosoft.com
        |
        v
Password / authentication method
        |
        v
Microsoft Entra authentication
```

Successful authentication means Microsoft has verified the identity.

It does **not** automatically mean the user is permitted to access every resource.

---

## 8. Authorization

**Authorization**, commonly shortened to **AuthZ**, determines what an authenticated user is allowed to access or perform.

Examples include:

- Access to a SharePoint site
- Membership in a Microsoft Team
- Administrative permissions
- Access to organizational resources
- Access granted through group membership

A useful distinction is:

```text
Authentication
= Who are you?

Authorization
= What are you allowed to access?
```

This distinction became important later in the project when Elena Rivera successfully authenticated but was denied access to a Finance SharePoint resource after her approved group-based access path was removed.

Therefore:

```text
Authenticated
        ≠
Authorized for every resource
```

---

## 9. Groups

A **group** organizes identities and can be used for supported access, collaboration, licensing, policy, or administrative scenarios.

Examples created later in the project included:

```text
SG-HR-Users
SG-Finance-Users
SG-Sales-Users
SG-IT-Users
SG-IT-Helpdesk
```

Groups allow administrators to manage access using a role or department model rather than configuring every individual user separately.

Example:

```text
Elena Rivera
      |
      v
SG-Finance-Users
      |
      v
Finance resource access
```

This supports more consistent administration and reduces unnecessary direct permissions.

---

## 10. Administrative Roles

An **administrative role** grants administrative permissions within Microsoft Entra ID or Microsoft 365.

Examples include:

- Global Administrator
- Helpdesk Administrator
- User Administrator
- Reports Reader
- Password Administrator

An administrative role is not the same thing as a normal security group.

Conceptually:

```text
Security Group
    |
    +-- Organizes users or access

Administrative Role
    |
    +-- Grants administrative capability
```

The tenant administrator initially used:

```text
Global Administrator
```

Later in the project, Pauline Hudson was assigned:

```text
Helpdesk Administrator
```

to demonstrate delegated administration and least privilege.

---

## 11. Group vs Administrative Role

The distinction between a group and an administrative role was important throughout the project.

### Group

Used primarily to organize identities and access.

Example:

```text
SG-IT-Helpdesk
```

Membership in this group did not automatically make Pauline a Microsoft Entra administrator.

### Administrative Role

Grants actual administrative privileges.

Example:

```text
Helpdesk Administrator
```

Pauline required a separate role assignment before she could perform approved Help Desk administrative operations.

Therefore:

```text
Group membership
        ≠
Administrative privilege
```

This prevented the lab from incorrectly treating security-group membership as equivalent to Microsoft Entra RBAC.

---

## 12. Identity vs License

A Microsoft Entra identity and a Microsoft 365 license are separate concepts.

### Identity

The user object exists in Microsoft Entra ID.

Example:

```text
Elena Rivera
erivera@abhinaylabs.onmicrosoft.com
```

### License

Provides entitlement to subscribed Microsoft 365 services.

A user can therefore exist without having a Microsoft 365 license.

Conceptually:

```text
Identity Created
      |
      +-- User can exist in Entra
      |
      +-- License may or may not be assigned
```

This distinction became an important troubleshooting scenario later in the project.

An unlicensed user was able to authenticate successfully but could not use Outlook because the required Exchange mailbox and service entitlement were not available.

Therefore:

```text
Identity exists
        ≠
Licensed for Microsoft 365

Authentication succeeds
        ≠
Service entitlement exists
```

---

## 13. AD DS vs Microsoft Entra ID

Microsoft Entra ID is not simply "Active Directory in the cloud."

The two technologies solve related identity problems but use different architectures.

| Active Directory Domain Services                    | Microsoft Entra ID                               |
| --------------------------------------------------- | ------------------------------------------------ |
| Primarily traditional on-premises directory service | Cloud identity and access management service     |
| Uses domain controllers                             | Microsoft-hosted cloud directory                 |
| Manages Windows domain identities                   | Manages cloud identities                         |
| Commonly uses Kerberos and LDAP                     | Uses modern cloud authentication protocols       |
| Supports Group Policy                               | Uses cloud identity, access, and policy controls |
| Domain-joined computers                             | Microsoft Entra registered/joined devices        |
| Commonly manages internal enterprise networks       | Commonly manages Microsoft 365 and SaaS access   |

The previous Active Directory lab used:

```text
abhinaylabs.internal
```

The Microsoft Entra tenant used:

```text
abhinaylabs.onmicrosoft.com
```

Initially, these were separate identity environments.

Later in the project, selected on-premises identities were synchronized to Microsoft Entra ID using Microsoft Entra Connect Sync.

---

## 14. Initial Lab State

At this stage of the project, the environment included:

```text
Tenant:
Abhinay Labs

Domain:
abhinaylabs.onmicrosoft.com

Microsoft Entra:
Microsoft Entra ID P1

Cloud Administrator:
admin@abhinaylabs.onmicrosoft.com

Administrative Role:
Global Administrator
```

The primary employee identities were still cloud-created.

Hybrid synchronization had not yet been implemented.

The environment also contained existing Microsoft 365 groups such as:

```text
Abhinay Labs
All Company
```

These default/existing collaboration groups were left intact while separate security groups were created later for the lab's access-management model.

---

## 15. Security Defaults and Authentication Context

During the initial cloud setup, Security Defaults were observed as enabled in the tenant. This describes the initial configuration state only; later security and Conditional Access work is documented separately, so the project does not claim that Security Defaults remained enabled throughout every later phase.

Microsoft Authenticator was also available as an authentication method within the environment.

These initial settings provided the starting security context for the cloud lab.

Later phases explored authentication-method configuration, MFA, administrative MFA, and Conditional Access in greater detail.

The important distinction established during this project was:

```text
Authentication method enabled by tenant
        ≠
Authentication method registered by every user
```

Tenant policy determines which methods users may be permitted to use.

Individual registration determines which methods are actually configured for a particular identity.

Later in the project, all four synthetic employee users completed Microsoft's required authentication-method/security-info registration flow. Pauline Hudson encountered this requirement after receiving the privileged Helpdesk Administrator role. The other synthetic employees also encountered a mandatory registration step later in the lab, but the exact policy or tenant setting that triggered their registration was not preserved as dedicated evidence.

---

## 16. Enterprise Relevance

Microsoft Entra ID is widely used in organizations that rely on Microsoft 365 and cloud applications.

Enterprise IT teams frequently use Entra ID to manage:

- Employee identities
- Authentication
- Administrative roles
- Group membership
- SaaS access
- Microsoft 365 access
- Device identities
- MFA
- Conditional Access
- Sign-in investigation
- Audit activity
- Hybrid identities

Understanding the basic identity model is therefore essential before attempting troubleshooting or administration.

---

## 17. IT Support Relevance

A Service Desk or IT Support technician may receive tickets such as:

```text
"I cannot sign in."

"I can sign in but Outlook does not work."

"I cannot access the Finance SharePoint site."

"My account is disabled."

"I lost my authentication device."

"I need access to a Microsoft Team."

"My Microsoft 365 apps are missing."
```

Each issue may involve a different layer.

A useful troubleshooting model is:

```text
Identity
   ↓
Account State
   ↓
Authentication
   ↓
Authorization
   ↓
Licensing
   ↓
Service Provisioning
   ↓
Policy
   ↓
Application / Client
```

Understanding Microsoft Entra fundamentals prevents technicians from treating every problem as a password-reset issue.

---

## 18. IAM and Security Relevance

Microsoft Entra ID directly supports core Identity and Access Management principles.

### Identity

Represents the user, device, application, or service.

### Authentication

Verifies the identity.

### Authorization

Determines permitted access.

### Role-Based Access Control

Administrative access can be granted according to job responsibilities.

### Least Privilege

Users and administrators should receive only the permissions required to perform their responsibilities.

### Group-Based Access

Access can be managed using groups rather than individually assigning permissions to every employee.

These concepts were implemented and tested throughout later phases of the project.

---

## 19. Evidence and Validation

This phase established the foundational tenant and identity concepts used throughout the remainder of the project. Dedicated implementation evidence is documented in the subsequent hands-on administration phases.

---

## 20. Key Lessons Learned

1. Microsoft Entra ID is Microsoft's cloud identity and access management platform.
2. A Microsoft tenant provides an isolated organizational cloud identity boundary.
3. Users, groups, devices, and applications are represented as directory objects.
4. A UPN commonly acts as the user's Microsoft cloud sign-in name.
5. Member identities normally represent internal organizational users, while Guest identities represent external collaboration users.
6. Authentication verifies identity; authorization determines permitted access.
7. Successful authentication does not guarantee access to a particular resource.
8. Security groups and administrative roles serve different purposes.
9. Group membership does not automatically provide administrative privilege.
10. A Microsoft Entra identity can exist without a Microsoft 365 license.
11. Microsoft Entra ID and Active Directory Domain Services are related but different identity platforms.
12. Understanding the identity layer is necessary before troubleshooting Microsoft 365 applications and services.

---

## 21. Phase Result

Phase 2 established the Microsoft Entra ID fundamentals required for the remainder of the project.

The phase covered:

- Microsoft Entra ID
- Microsoft tenants
- Directory objects
- User Principal Names
- Member and Guest identities
- Authentication
- Authorization
- Security groups
- Administrative roles
- Identity versus licensing
- AD DS versus Microsoft Entra ID
- IAM and least-privilege concepts
- Enterprise IT Support relevance

These concepts became the foundation for later hands-on work involving users, groups, licensing, authentication troubleshooting, Microsoft 365 services, RBAC, Conditional Access, device identity, PowerShell, and hybrid identity.

**Phase 2 Status: COMPLETE**


