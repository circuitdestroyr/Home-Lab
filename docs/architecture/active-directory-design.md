# Active Directory Design

## Purpose

This document defines the Active Directory structure for the Cyber Enterprise Lab.

The goal is to create a realistic small business Active Directory environment that supports security monitoring, attack simulation, and incident response exercises.

---

# Domain Information

| Item | Value |
|---|---|
| Domain Name | TBD |
| Forest Name | TBD |
| Domain Controller | DC01 |
| DNS Server | DC01 |
| Functional Level | TBD |

---

# Domain Controller

| Hostname | Role | Status |
|---|---|---|
| DC01 | Active Directory Domain Controller / DNS | Operational |

---

# Organizational Unit Design

Planned OU structure:

```text
CyberEnterprise.local
│
├── Users
│   ├── Employees
│   ├── Administrators
│   └── Service Accounts
│
├── Computers
│   ├── Workstations
│   └── Servers
│
├── Groups
│
└── Security
    ├── SOC
    └── Audit

# User Groups

Planned groups:

| Group | Purpose |
|---|---|
| Domain Admins | Administrative management |
| IT Admins | Infrastructure administration |
| SOC Analysts | Security monitoring |
| Employees | Standard user accounts |
| Service Accounts | Application/service identities |

---

# Security Considerations

Future configuration will include:

- Least privilege access
- Separate administrative accounts
- Group Policy security controls
- Audit logging
- Authentication monitoring
- Detection engineering scenarios
