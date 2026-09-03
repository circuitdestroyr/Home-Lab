# Cyber Enterprise Lab — Continuation Statement

GitHub repository is the source of truth.

## Current Project Phase

Security Visibility Foundation

## Current Stopping Point

The basic Windows telemetry pipeline is now VERIFIED.

CLIENT01 is successfully sending Windows Application, Security, and System Event Logs through the Splunk Universal Forwarder to SPLUNK01 over TCP 9997. Splunk is receiving, indexing, and returning the events through search.

The next milestone is Sysmon deployment.

---

# VERIFIED LAB FOUNDATION

## DC01

- Windows Server 2022
- Active Directory Domain Services
- DNS
- `homelab.local`
- IP: `192.168.15.10`
- Operational and verified
- External DNS forwarders configured
- External DNS resolution verified

## CLIENT01

- Windows 11 Pro
- IP: `192.168.15.20`
- Joined `homelab.local`
- Domain authentication verified
- Secure channel verified
- Active Directory computer object verified
- DNS points to DC01
- Connectivity to SPLUNK01 verified
- Post-domain-join VM snapshot still needs physical verification

## SPLUNK01

- VMware VM on Windows laptop
- Ubuntu Server 24.04 LTS
- 4 vCPU
- 6 GB RAM
- 80 GB storage
- Static IP: `192.168.15.30`
- Gateway: `192.168.15.2`
- DNS: `192.168.15.10`
- VMware NAT
- OpenSSH installed
- SSH remote administration verified
- Gateway connectivity verified
- DC01 connectivity verified
- DC01 DNS resolution verified
- External DNS resolution through DC01 verified
- Clean SPLUNK01 baseline VMware snapshot created

---

# SPLUNK ENTERPRISE

- Splunk Enterprise 10.4.2 installed
- Debian package integrity verified using published SHA-512 checksum
- Splunk administrator account created
- Splunk Web verified
- HTTP port 8000 verified
- Management port 8089 verified
- `splunkd` service verified running
- Boot-start configured
- `/etc/init.d/splunk` created
- Splunk receiving enabled on TCP 9997
- SPLUNK01 confirmed listening on `0.0.0.0:9997`

---

# UNIVERSAL FORWARDER

CLIENT01:

- Splunk Universal Forwarder 10.4.2 installed
- Universal Forwarder service verified Running
- Windows service account: Local System
- SeBackupPrivilege enabled
- SeSecurityPrivilege enabled
- Performance Monitor Users enabled
- Application Event Log selected
- Security Event Log selected
- System Event Log selected
- Performance Monitor collection not enabled
- Deployment Server not configured
- Receiving indexer configured as `192.168.15.30:9997`
- UF administrator account: `ufadmin`
- Active forward to `192.168.15.30:9997` verified

---

# WINDOWS TELEMETRY VERIFICATION

A controlled Application event was generated on CLIENT01:

- Source: `CyberLab`
- Event ID: `1000`
- Message: `Cyber Enterprise Lab telemetry test - CLIENT01`

The event was verified locally on CLIENT01.

The same event was successfully located in Splunk.

Verified metadata:

- Host: `CLIENT01`
- Source: `WinEventLog:Application`
- Sourcetype: `WinEventLog:Application`
- Index: `main`

Additional Splunk verification confirmed all three configured Windows Event Log channels are being ingested:

| Windows Log | Splunk Source | Events Observed |
|---|---|---:|
| Application | `WinEventLog:Application` | 18 |
| Security | `WinEventLog:Security` | 397 |
| System | `WinEventLog:System` | 19 |

## Verified Telemetry Pipeline

CLIENT01
    |
    | Windows Event Logs
    v
Splunk Universal Forwarder
    |
    | TCP 9997
    v
SPLUNK01
    |
    v
Splunk Enterprise
    |
    v
main index
    |
    v
Splunk Search

## Telemetry Status

Windows Application, Security, and System Event Log ingestion: VERIFIED

Do not treat Sysmon telemetry as verified yet.

---

# IMPORTANT ARCHITECTURE RULES

Do not rebuild or move SPLUNK01.

SPLUNK01 belongs on the Windows laptop and is already operational.

Do not change the existing DNS architecture.

DC01 remains the DNS server for the lab.

Do not begin detection engineering until the Sysmon telemetry baseline is established.

---

# NEXT SESSION — START HERE

1. Verify/create the CLIENT01 pre-Sysmon VMware snapshot.
2. Download the official Microsoft Sysmon package.
3. Install Sysmon on CLIENT01.
4. Configure useful security telemetry.
5. Verify the Sysmon service.
6. Verify the Sysmon event channel locally.
7. Confirm the Universal Forwarder collects the Sysmon channel.
8. Verify Sysmon events arrive in Splunk.
9. Identify the resulting Splunk fields and sourcetype.
10. Document the Sysmon telemetry pipeline.
11. Commit and push documentation changes.
12. Begin detection engineering only after Sysmon telemetry is verified.

---

# CURRENT BLOCKERS

None.

## Known Remaining Verification

- Confirm post-domain-join CLIENT01 VM snapshot exists
- Deploy Sysmon
- Verify Sysmon telemetry
- Document Sysmon telemetry
- Begin detection engineering

---

# WORKFLOW

Design → Document → Build → Verify → Commit

---

# END STATE FOR TONIGHT

The Windows telemetry foundation is operational and verified.

DC01 is healthy.

CLIENT01 is domain joined and healthy.

SPLUNK01 is operational.

Splunk Enterprise is running.

Splunk receiving is enabled on TCP 9997.

The Universal Forwarder is installed and running on CLIENT01.

CLIENT01 has an active forwarding connection to SPLUNK01.

Application, Security, and System Windows Event Logs are successfully indexed and searchable in Splunk.

The next session begins with the CLIENT01 pre-Sysmon snapshot checkpoint, followed by Sysmon deployment and telemetry verification.
