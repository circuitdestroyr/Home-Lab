# Project Status

## Current Phase

Current Phase:
Security Visibility Foundation

---

## Current Milestone

Complete Active Directory integration for CLIENT01 by:

- CLIENT01 Domain Integration
- Configuring CLIENT01 networking
- Pointing DNS to DC01
- Joining homelab.local
- Verifying domain authentication
- Creating a post-domain-join VM snapshot

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

Status: Operational

Completed:
- Windows 11 Pro installed
- VMware VM created
- TPM configured
- Secure Boot enabled
- Hostname assigned as CLIENT01
- Local administrative account created
- Windows installation completed successfully

Pending:
- Active Directory domain join
- DNS validation
- Domain authentication testing

---

## In Progress

- [ ] Configure CLIENT01 networking
- [ ] Join CLIENT01 to homelab.local
- [ ] Verify domain authentication

## Upcoming

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
| CLIENT01 | Windows Domain Workstation | Operational |
| SPLUNK01 | Security Monitoring Platform | Planned |
| KALI01 | Attack Simulation Workstation | Planned |
| FG01 | Firewall | Planned |
| JNPR01 | Network Infrastructure | Planned |

## Blockers

None

## Last Updated

2026-08-04
