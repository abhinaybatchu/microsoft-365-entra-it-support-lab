# Phase 1 — Microsoft 365 Lab Environment

## 1. Objective

The objective of this phase was to create an isolated Microsoft 365 tenant for hands-on cloud identity, Microsoft 365 administration, security, and IT Support practice.

The environment was built for the fictional organization **Abhinay Labs** and later became the cloud side of a hybrid identity lab connected to the existing on-premises Active Directory environment.

---

## 2. Environment Overview

The Microsoft 365 environment was created using:

| Component                    | Configuration                                          |
| ---------------------------- | ------------------------------------------------------ |
| Organization                 | Abhinay Labs                                           |
| Microsoft 365 tenant         | `abhinaylabs.onmicrosoft.com`                          |
| Subscription                 | Microsoft 365 Business Premium Trial                   |
| Available licenses           | 25                                                     |
| Microsoft Entra edition      | Microsoft Entra ID P1                                  |
| Administrative account       | `admin@abhinaylabs.onmicrosoft.com`                    |
| Administrative role          | Global Administrator                                   |
| Primary administration model | Microsoft 365 and Microsoft Entra cloud administration |

The tenant was intentionally created using fictional organizational information and synthetic employee identities.

---

## 3. Why the Lab Was Created

Modern enterprise IT Support teams frequently work with Microsoft 365 and Microsoft Entra ID rather than relying entirely on traditional on-premises Active Directory.

Common support responsibilities include:

- Creating and managing user identities
- Resetting passwords
- Troubleshooting authentication
- Managing Microsoft 365 licenses
- Supporting Exchange Online mailboxes
- Supporting Microsoft Teams
- Troubleshooting SharePoint and OneDrive access
- Managing group memberships
- Investigating sign-in activity
- Supporting MFA
- Working with Microsoft Entra administrative roles
- Investigating service-health incidents
- Escalating problems with useful technical evidence

This tenant provided a controlled environment to practice those tasks without affecting a real organization.

---

## 4. Microsoft 365 Tenant

A Microsoft 365 tenant represents an organization's isolated Microsoft cloud environment.

The lab tenant was:

```text
abhinaylabs.onmicrosoft.com
```

The tenant became the central cloud environment for:

```text
Microsoft Entra ID
        |
        +-- Users
        +-- Groups
        +-- Administrative Roles
        +-- Authentication
        +-- Conditional Access
        +-- Device Identities
        |
        +-- Microsoft 365 Services
                |
                +-- Exchange Online
                +-- Microsoft Teams
                +-- SharePoint Online
                +-- OneDrive
```

Later in the project, the tenant was connected to the existing on-premises Active Directory environment through Microsoft Entra Connect Sync.

---

## 5. Administrative Account

The tenant administrative account used for configuration was:

```text
admin@abhinaylabs.onmicrosoft.com
```

The account held the:

```text
Global Administrator
```

role.

The Global Administrator account was used only where tenant-level administrative access was required.

A separate synthetic IT Support identity was later assigned the narrower **Helpdesk Administrator** role to demonstrate least-privilege administration.

This distinction was important because routine support operations should not require unrestricted tenant administration.

---

## 6. Microsoft 365 Business Premium

Microsoft 365 Business Premium was selected because it provided the Microsoft 365 and identity capabilities required for the project.

The subscription enabled hands-on work with services including:

- Microsoft Entra ID
- Exchange Online
- Microsoft Teams
- SharePoint Online
- OneDrive
- Microsoft 365 applications
- Microsoft Entra ID P1 features

The tenant contained 25 available licenses during the trial.

Licenses were intentionally assigned in a controlled manner rather than automatically licensing every synthetic user.

This later allowed the lab to demonstrate the difference between:

```text
Identity exists
        ≠
Microsoft 365 service is licensed
        ≠
Service is fully provisioned
```

---

## 7. Administrative Portals

Several Microsoft administrative portals were used throughout the project.

### Microsoft 365 Admin Center

Used for:

- Active user administration
- Microsoft 365 licensing
- Password and sign-in administration
- Service Health
- OneDrive administrative functions
- General Microsoft 365 tenant administration

### Microsoft Entra Admin Center

Used for:

- Identity administration
- Security groups
- Administrative roles
- Authentication methods
- Sign-in logs
- Audit logs
- Conditional Access
- Device identities
- Hybrid identity validation

### Exchange Admin Center

Used for:

- Mailbox validation
- Email forwarding
- Exchange Online administration

### Microsoft Teams Admin Center

Used for:

- User policy inspection
- Messaging policy configuration
- Teams-related support validation

### SharePoint and OneDrive

Used for:

- SharePoint site permissions
- File access
- Team-content validation
- OneDrive administrative access

---

## 8. Initial Cloud Identity Model

The project initially used cloud-native Microsoft Entra identities.

The primary fictional employees were:

| Employee       | Initial Cloud UPN                     | Department             |
| -------------- | ------------------------------------- | ---------------------- |
| David Miller   | `dmiller@abhinaylabs.onmicrosoft.com` | Human Resources        |
| Elena Rivera   | `erivera@abhinaylabs.onmicrosoft.com` | Finance                |
| Joseph Daniel  | `jdaniel@abhinaylabs.onmicrosoft.com` | Sales                  |
| Pauline Hudson | `phudson@abhinaylabs.onmicrosoft.com` | Information Technology |

At this stage, these identities were:

```text
Cloud-created
On-premises sync enabled: No
```

This was intentional.

The project first established a clean understanding of Microsoft 365 and Microsoft Entra ID before adding hybrid synchronization later.

---

## 9. Security Considerations

The lab followed several security principles from the beginning.

### Synthetic Identities

All employee identities were fictional.

### Credential Protection

Public documentation excludes:

- Passwords
- Temporary passwords
- MFA secrets
- Authentication tokens
- Recovery information
- Personal contact information
- Payment information

### Least Privilege

The Global Administrator account was retained for tenant-level configuration, while routine Help Desk administration was later delegated through a narrower Microsoft Entra role.

### Controlled Testing

Security and access changes were tested using controlled lab scenarios rather than applying unnecessary broad configuration changes.

---

## 10. Enterprise Relevance

A Microsoft 365 tenant is a common environment for modern enterprise IT Support.

Support technicians may need to work across multiple portals when troubleshooting a single issue.

For example:

```text
User cannot access Outlook
        |
        +-- Is the Entra identity enabled?
        +-- Can the user authenticate?
        +-- Does the user have a license?
        +-- Is Exchange Online provisioned?
        +-- Is Microsoft reporting a service incident?
        +-- Is the issue specific to the client/session?
```

This project was designed around that layered troubleshooting model rather than treating every Microsoft 365 problem as a simple password issue.

---

## 11. IT Support Relevance

This environment supports practical Service Desk and IT Support activities such as:

- User provisioning
- Account enable/disable operations
- Password resets
- Authentication troubleshooting
- License assignment
- Mailbox support
- Teams support
- SharePoint and OneDrive access troubleshooting
- Group membership administration
- MFA assistance
- Sign-in log investigation
- Service-health investigation
- Ticket escalation
- Joiner, Mover, and Leaver workflows

---

## 12. Security and IAM Relevance

The Microsoft 365 environment also introduced several IAM concepts that became important throughout the project.

### Authentication

Authentication verifies who the user is.

### Authorization

Authorization determines what the authenticated user can access.

### Licensing

Licensing determines which Microsoft 365 services the identity is entitled to use.

### Administrative Roles

Microsoft Entra roles determine what administrative actions an identity is permitted to perform.

### Least Privilege

Support personnel should receive only the administrative permissions required for their responsibilities.

These concepts were validated through practical troubleshooting later in the project.

---

## 13. Relationship to the Existing Active Directory Lab

The previous Active Directory IT Support Lab represented the traditional on-premises identity environment:

```text
Windows Server
    ↓
Active Directory Domain Services
    ↓
Domain Controllers
    ↓
Domain Users and Computers
```

Project 2 initially created a separate Microsoft cloud identity environment:

```text
Microsoft 365
    ↓
Microsoft Entra ID
    ↓
Cloud Users and Groups
    ↓
Microsoft 365 Services
```

Later phases connected the two environments using Microsoft Entra Connect Sync.

This created the final architecture:

```text
On-Premises AD DS
        |
        | Microsoft Entra Connect Sync
        | Password Hash Synchronization
        |
        v
Microsoft Entra ID
        |
        v
Microsoft 365 Services
```

The hybrid deployment was intentionally limited to a controlled set of employee identities rather than synchronizing the entire Active Directory environment.

---

## 14. Evidence and Validation

This phase established the foundational tenant and identity concepts used throughout the remainder of the project. Dedicated implementation evidence is documented in the subsequent hands-on administration phases.

---

## 15. Key Lessons Learned

1. A Microsoft 365 tenant is the organization's isolated Microsoft cloud environment.
2. Microsoft Entra ID provides cloud identity and access management for Microsoft 365 and other applications.
3. Creating an identity does not automatically provide access to every Microsoft 365 service.
4. Microsoft 365 licensing and service provisioning are separate from basic identity creation.
5. Microsoft cloud administration is distributed across multiple specialized admin portals.
6. Routine support tasks should follow least privilege rather than relying on Global Administrator access.
7. Cloud-native administration should be understood before introducing hybrid identity synchronization.
8. Synthetic identities and controlled scenarios allow realistic administration without exposing real organizational information.

---

## 16. Phase Result

Phase 1 successfully established the Microsoft 365 cloud lab used throughout the remainder of the project.

The environment provided:

- A Microsoft 365 Business Premium tenant
- Microsoft Entra ID
- A Global Administrator account
- Four synthetic employee identities
- Microsoft 365 administrative portals
- Microsoft 365 service access
- A controlled foundation for identity, licensing, authentication, security, troubleshooting, device identity, PowerShell, and later hybrid identity administration

**Phase 1 Status: COMPLETE**
