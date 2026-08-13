# Project Status

## Current Phase

Current Phase:
Security Visibility Foundation

---
## Current Milestone

Complete Active Directory integration for CLIENT01.

Completed:

- CLIENT01 Domain Integration
- Configuring CLIENT01 networking
- Pointing DNS to DC01
- Joining homelab.local
- Verifying domain authentication

Remaining Verification:

- Confirm post-domain-join VM snapshot exists
## Current Environment Status

### DC01

Status: Operational

Completed:
- Windows Server 2022 installed
- Active Directory Domain Services installed
- Domain created
- DNS configured
- SYSVOL verified
- NETLOGON verified
- Domain Controller health checks completed

---

### CLIENT01

Status:
Complete

CLIENT01:

Hostname:
CLIENT01

Operating System:
Windows 11 Pro

Role:
Standard Employee Workstation / User Endpoint

Resources:

- 2 CPU cores
- 4 GB RAM
- 64 GB storage

Network:

- VMware NAT
- Same VMware network as DC01


Purpose:

Provide a realistic enterprise endpoint for:

- Authentication events
- Security logging
- Detection engineering
- Incident response scenarios


Completed CLIENT01 tasks:

- Windows 11 Pro installation
- VMware VM creation
- TPM configured
- Secure Boot enabled
- Hostname assigned
- Local administrative account created
- Network configured
- DNS pointed to DC01
- Active Directory discovery verified
- Joined homelab.local domain
- Domain authentication verified
- Secure channel verified


CLIENT01 Verification Results:

Domain Membership:

Command:

systeminfo | findstr /B /C:"Domain"

Result:

Domain: homelab.local


Authentication:

Command:

whoami

Result:

homelab\administrator


Secure Channel:

Command:

Test-ComputerSecureChannel

Result:

True


Active Directory verification:

CLIENT01 computer object confirmed in:

homelab.local
└── Computers
    └── CLIENT01


Remaining Verification:

- Confirm post-domain-join VM snapshot exists

### Identity and Administration
- Domain users and groups
- Organizational Units (OUs)
- Group Policy configuration
- Administrative account structure

### Security Operations
- Splunk Enterprise deployment
- Windows event collection
- Sysmon deployment
- Linux log collection
- Firewall log collection

### Network Infrastructure
- FortiGate firewall deployment
- Juniper networking deployment
- Network segmentation
- Security monitoring

### Cybersecurity Scenarios
- MITRE ATT&CK-based attack simulations
- Detection engineering
- Alert creation and tuning
- Incident response investigations
- Lessons learned documentation

## Environment Status

| System | Purpose | Status |
|---|---|---|
| DC01 | Active Directory Domain Controller / DNS | Operational |
| CLIENT01 | Windows Domain Workstation | Operational — Domain Joined |
| SPLUNK01 | Security Monitoring Platform | Planned |
| KALI01 | Attack Simulation Workstation | Planned |
| FG01 | Firewall | Planned |
| JNPR01 | Network Infrastructure | Planned |

## Blockers

None

## Last Updated

2026-08-13
