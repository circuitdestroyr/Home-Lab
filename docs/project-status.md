# Project Status

## Current Phase

Security Visibility Foundation

---

## Current Milestone

Build the SPLUNK01 security monitoring foundation and prepare the lab for Windows telemetry collection.

### Completed

- CLIENT01 networking configured
- DNS configured to use DC01
- Active Directory discovery verified
- CLIENT01 joined to `homelab.local`
- Domain authentication verified
- Secure channel verified
- CLIENT01 computer object verified in Active Directory
- SPLUNK01 VMware VM deployed
- Ubuntu Server 24.04 LTS installed
- SPLUNK01 static networking configured
- SPLUNK01 gateway connectivity verified
- SPLUNK01 connectivity to DC01 verified
- SPLUNK01 internal DNS resolution verified
- SPLUNK01 external DNS resolution through DC01 verified
- SSH remote administration verified
- SPLUNK01 system updates completed
- Clean SPLUNK01 baseline VMware snapshot created

### Remaining Verification

- Confirm post-domain-join CLIENT01 VM snapshot exists
- Install Splunk Enterprise on SPLUNK01
- Verify Splunk service and web interface
- Configure Windows telemetry collection

---

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

Status: Operational — Domain Joined

**Hostname:** CLIENT01

**Operating System:** Windows 11 Pro

**Role:** Standard Employee Workstation / User Endpoint

**Resources:**

- 2 CPU cores
- 4 GB RAM
- 64 GB storage

**Network:**

- VMware NAT
- Same VMware network as DC01

### Purpose

Provide a realistic enterprise endpoint for:

- Authentication events
- Security logging
- Detection engineering
- Incident response scenarios

### Completed CLIENT01 Tasks

- Windows 11 Pro installation
- VMware VM creation
- TPM configured
- Secure Boot enabled
- Hostname assigned
- Local administrative account created
- Network configured
- DNS pointed to DC01
- Active Directory discovery verified
- Joined `homelab.local` domain
- Domain authentication verified
- Secure channel verified
- CLIENT01 computer object confirmed in Active Directory

### CLIENT01 Verification Results

**Domain Membership**

Command:

```powershell
systeminfo | findstr /B /C:"Domain"
```

Result:

```text
Domain: homelab.local
```

**Authentication**

Command:

```powershell
whoami
```

Result:

```text
homelab\administrator
```

**Secure Channel**

Command:

```powershell
Test-ComputerSecureChannel
```

Result:

```text
True
```

**Active Directory Verification**

CLIENT01 computer object confirmed in:

```text
homelab.local
└── Computers
    └── CLIENT01
```

### Remaining Verification

- Confirm post-domain-join VM snapshot exists

---

## SPLUNK01 Foundation

Status:
In Progress — OS installed, network configured

SPLUNK01:

Hostname:
SPLUNK01

Operating System:
Ubuntu Server 24.04 LTS

Role:
SIEM / Security Monitoring

IP:
192.168.15.30

Gateway:
192.168.15.2

DNS:
192.168.15.10

Network:
VMware NAT

Resources:

- 4 vCPU
- 6 GB RAM
- 80 GB storage

Current state:

- Ubuntu Server installed
- OpenSSH server installed
- Static IP configured
- Gateway connectivity verified
- DC01 connectivity verified
- Active Directory DNS resolution verified
- Ubuntu system updates completed
- SSH remote administration verified
- Clean SPLUNK01 baseline snapshot created
- DC01 external DNS resolution troubleshooting completed
- DC01 DNS forwarders configured
- External Splunk domain resolution through DC01 verified
- Splunk Enterprise not yet installed
- Windows telemetry collection not yet configured

---

## Identity and Administration

Planned:

- Domain users and groups
- Organizational Units (OUs)
- Group Policy configuration
- Administrative account structure

---

## Security Operations

Current:

- SPLUNK01 base system deployed
- Splunk Enterprise installation pending

Planned:

- Windows event collection
- Sysmon deployment
- Linux log collection
- Firewall log collection
- Detection engineering
- Alert creation and tuning

---

## Network Infrastructure

Planned:

- FortiGate firewall deployment
- Juniper networking deployment
- Network segmentation
- Security monitoring

---

## Cybersecurity Scenarios

Planned:

- MITRE ATT&CK-based attack simulations
- Detection engineering
- Alert creation and tuning
- Incident response investigations
- Lessons learned documentation

---

## Environment Status

| System | Purpose | Status |
|---|---|---|
| DC01 | Active Directory Domain Controller / DNS | Operational |
| CLIENT01 | Windows Domain Workstation | Operational — Domain Joined |
| SPLUNK01 | Security Monitoring Platform | In Progress |
| KALI01 | Attack Simulation Workstation | Planned |
| FG01 | Firewall | Planned |
| JNPR01 | Network Infrastructure | Planned |

---

## Blockers

None

---

## Last Updated

2026-08-21