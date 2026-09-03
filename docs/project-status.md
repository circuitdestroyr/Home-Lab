# Project Status

## Current Phase

Security Visibility Foundation

---

## Current Milestone

Build the SPLUNK01 security monitoring foundation and establish the initial Windows telemetry pipeline.

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
- DC01 DNS forwarders configured
- Splunk Enterprise 10.4.2 installed on SPLUNK01
- Splunk administrator account created
- Splunk Web interface verified on port 8000
- Splunk management port verified on 8089
- Splunk service verified running
- Splunk configured for boot-start
- Splunk receiving configured on TCP port 9997
- CLIENT01 connectivity to SPLUNK01 TCP port 9997 verified
- Splunk Universal Forwarder 10.4.2 installed on CLIENT01
- Universal Forwarder configured to send data to SPLUNK01
- Application, Security, and System Windows Event Logs selected for collection
- Universal Forwarder Windows service verified running

### Remaining Work

- Confirm post-domain-join CLIENT01 VM snapshot exists
- Deploy Sysmon
- Verify Sysmon events in Splunk
- Document Sysmon telemetry
- Begin detection engineering

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
- External DNS forwarders configured
- External DNS resolution verified

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
- IP address: `192.168.15.20`
- DNS server: `192.168.15.10`
- Same VMware network as DC01 and SPLUNK01

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
- Connectivity to SPLUNK01 verified
- TCP connectivity to SPLUNK01 port 8089 verified
- TCP connectivity to SPLUNK01 port 9997 verified
- Splunk Universal Forwarder 10.4.2 installed
- Universal Forwarder configured for on-premises Splunk Enterprise
- Receiving indexer configured as `192.168.15.30:9997`
- Application, Security, and System Windows Event Logs selected
- Universal Forwarder service verified running

### CLIENT01 Verification Results

**Domain Membership**

Command:

`systeminfo | findstr /B /C:"Domain"`

Result:

`Domain: homelab.local`

**Authentication**

Command:

`whoami`

Result:

`homelab\administrator`

**Secure Channel**

Command:

`Test-ComputerSecureChannel`

Result:

`True`

**Active Directory Verification**

CLIENT01 computer object confirmed in:

`homelab.local`
`└── Computers`
`    └── CLIENT01`

**Domain Controller Discovery**

Command:

`nltest /dsgetdc:homelab.local`

Result:

DC01 successfully located at `192.168.15.10`.

**DNS Verification**

Command:

`nslookup dc01.homelab.local`

Result:

`dc01.homelab.local` resolved to `192.168.15.10`.

**Active Directory SRV Verification**

Command:

`nslookup -type=SRV _ldap._tcp.dc._msdcs.homelab.local`

Result:

LDAP service record successfully resolved to `dc01.homelab.local` on port `389`.

### Windows Telemetry Status

Universal Forwarder installation is complete and the service is running.

Current telemetry configuration:

- Application Event Log collection selected
- Security Event Log collection selected
- System Event Log collection selected
- Receiving indexer configured as `192.168.15.30:9997`

### Verification Results

- Network connectivity to SPLUNK01: Verified
- TCP 9997 connectivity: Verified
- Universal Forwarder service: Running
- Active forward to `192.168.15.30:9997`: Verified
- Application Event Log ingestion: Verified
- Security Event Log ingestion: Verified
- System Event Log ingestion: Verified
- Splunk indexing: Verified
- CLIENT01 events searchable in Splunk: Verified

Verified Splunk telemetry:

| Windows Log | Source | Events Observed |
|---|---|---:|
| Application | `WinEventLog:Application` | 18 |
| Security | `WinEventLog:Security` | 397 |
| System | `WinEventLog:System` | 19 |

Verified test event:

- Host: `CLIENT01`
- Source: `WinEventLog:Application`
- Sourcetype: `WinEventLog:Application`
- Index: `main`
- Event source: `CyberLab`
- Event ID: `1000`

### Telemetry Pipeline

`CLIENT01 → Windows Event Logs → Splunk Universal Forwarder → TCP 9997 → SPLUNK01 → main index → Splunk Search`

**Windows Event Log telemetry is VERIFIED.**

### Remaining Work

- Confirm post-domain-join VM snapshot exists
- Deploy Sysmon after the verified Windows telemetry baseline
- Verify Sysmon telemetry in Splunk

---

## SPLUNK01 Foundation

Status:

Operational — Splunk Enterprise installed and running

**Hostname:** SPLUNK01

**Operating System:** Ubuntu Server 24.04 LTS

**Role:** SIEM / Security Monitoring

**IP:** `192.168.15.30`

**Gateway:** `192.168.15.2`

**DNS:** `192.168.15.10`

**Network:** VMware NAT

**Resources:**

- 4 vCPU
- 6 GB RAM
- 80 GB storage

### Current State

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
- Splunk Enterprise 10.4.2 installed
- Splunk administrator account created
- Splunk Web interface verified on port 8000
- Splunk management port verified on port 8089
- Splunk service verified running
- Splunk configured for boot-start
- Splunk receiving enabled on TCP port 9997
- CLIENT01 TCP connectivity to port 9997 verified

### Splunk Telemetry Status

SPLUNK01 is receiving forwarded Windows Event Logs from CLIENT01.

Verified data flow:

CLIENT01
→ Splunk Universal Forwarder
→ TCP 9997
→ SPLUNK01
→ Splunk Enterprise
→ `main` index
→ Splunk Search

Application, Security, and System Windows Event Logs have been verified as searchable in Splunk.

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
- Splunk Enterprise 10.4.2 installed and operational
- Splunk receiving configured on TCP 9997
- CLIENT01 Universal Forwarder installed and running
- Application, Security, and System Windows Event Log ingestion verified
- CLIENT01 telemetry searchable in Splunk `main` index
- Basic Splunk searches performed
- Windows telemetry pipeline documented

Planned:

- Sysmon deployment
- Sysmon telemetry verification
- Linux log collection
- Firewall log collection
- Detection engineering
- Alert creation and tuning
- Incident response investigations

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
| CLIENT01 | Windows Domain Workstation / Telemetry Source | Operational — UF Running |
| SPLUNK01 | Security Monitoring Platform | Operational — Splunk Running |
| KALI01 | Attack Simulation Workstation | Planned |
| FG01 | Firewall | Planned |
| JNPR01 | Network Infrastructure | Planned |

---

## Blockers

None

---

## Next Session

1. Verify/create the CLIENT01 pre-Sysmon VMware snapshot.
2. Deploy Sysmon on CLIENT01.
3. Configure Sysmon security telemetry.
4. Verify the Sysmon service and local event generation.
5. Verify Sysmon events in Splunk.
6. Document the Sysmon telemetry pipeline.
7. Commit and push documentation.
8. Begin detection engineering.

---

## Last Updated

2026-09-03
