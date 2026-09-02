Cyber Enterprise Lab — Continuation Statement

GitHub repository is the source of truth.

Current project phase:
Security Visibility Foundation

CURRENT STOPPING POINT

SPLUNK01 is operational with Splunk Enterprise installed and running.

CLIENT01 has the Splunk Universal Forwarder installed and running.

SPLUNK01 is configured to receive forwarded data on TCP 9997.

CLIENT01 can successfully communicate with SPLUNK01 on TCP 9997.

The next task is to verify that Windows Event Logs are actually being forwarded from CLIENT01 and indexed by Splunk.

COMPLETED LAB FOUNDATION

DC01
- Windows Server 2022
- Active Directory Domain Services
- DNS
- homelab.local
- IP: 192.168.15.10
- Operational and verified
- External DNS forwarders configured
- External DNS resolution verified

CLIENT01
- Windows 11 Pro
- IP: 192.168.15.20
- Joined homelab.local
- Domain authentication verified
- Secure channel verified
- AD computer object verified
- DNS points to DC01
- Post-domain-join VM snapshot still needs physical verification

SPLUNK01
- VMware VM on Windows laptop
- Ubuntu Server 24.04 LTS
- 4 vCPU
- 6 GB RAM
- 80 GB storage
- Static IP: 192.168.15.30
- Gateway: 192.168.15.2
- DNS: 192.168.15.10
- VMware NAT
- OpenSSH installed
- SSH remote administration verified
- Gateway connectivity verified
- DC01 connectivity verified
- DC01 DNS resolution verified
- External DNS resolution through DC01 verified
- DC01 DNS forwarders configured
- Clean SPLUNK01 baseline VMware snapshot created

SPLUNK ENTERPRISE
- Splunk Enterprise 10.4.2 installed
- Debian package integrity verified using published SHA-512 checksum
- Splunk administrator account created
- Splunk Web verified
- HTTP port 8000 verified
- Management port 8089 verified
- splunkd service verified running
- Boot-start configured
- `/etc/init.d/splunk` created
- Splunk installation operational
- Receiving enabled on TCP 9997

CLIENT01 → SPLUNK01 NETWORK VERIFICATION

Verified from CLIENT01:

- Ping to 192.168.15.30 successful
- 0% packet loss
- TCP 8089 connectivity successful
- TCP 9997 connectivity successful

UNIVERSAL FORWARDER

- Splunk Universal Forwarder 10.4.2 installed on CLIENT01
- On-premises deployment selected
- Installation completed on CLIENT01 VM
- Windows service account: Local System
- SeBackupPrivilege enabled
- SeSecurityPrivilege enabled
- Performance Monitor Users enabled
- Application Event Log selected
- Security Event Log selected
- System Event Log selected
- Performance Monitor collection not enabled
- Deployment Server not configured
- Receiving indexer configured as:
  192.168.15.30:9997
- UF administrator account created:
  ufadmin
- SplunkForwarder service verified as Running

CURRENT TELEMETRY STATE

The intended data flow is:

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
Splunk Search / Detection Engineering

Network connectivity to the receiving port is verified.

Universal Forwarder installation and service status are verified.

Actual Windows Event Log ingestion into Splunk has NOT yet been verified.

DO NOT CLAIM TELEMETRY INGESTION IS COMPLETE YET.

DOCUMENTATION

GitHub repository has been updated.

Updated:
- docs/build-log.md
  - Session 7 — CLIENT01 Telemetry Preparation
- docs/project-status.md
  - Updated SPLUNK01 status
  - Updated CLIENT01 telemetry status
  - Updated Security Operations status
  - Updated next-session tasks

Documentation should remain synchronized with verified lab state.

ARCHITECTURE RULE

Do not rebuild or move SPLUNK01.

SPLUNK01 belongs on the Windows laptop and is already operational.

Do not change the existing DNS architecture.

DC01 remains the DNS server for the lab.

NEXT SESSION — START HERE

1. Verify CLIENT01 Universal Forwarder configuration.
2. Confirm the Windows Event Log inputs are configured correctly.
3. Confirm the forwarding destination is `192.168.15.30:9997`.
4. Verify the Universal Forwarder is actively forwarding.
5. Search Splunk for CLIENT01 events.
6. Confirm Application, Security, and System events are being indexed.
7. Troubleshoot only if actual ingestion fails.
8. Document the verified telemetry pipeline.
9. Commit and push any resulting documentation changes.
10. After basic Windows Event Logs are confirmed, deploy Sysmon.
11. Verify Sysmon events in Splunk.

IMPORTANT

Do not begin detection engineering yet.

First prove:

CLIENT01 → UF → TCP 9997 → SPLUNK01 → indexed Windows events

Once that pipeline is confirmed, we can move into Sysmon and then detection engineering.

WORKFLOW

Design → Document → Build → Verify → Commit

CURRENT BLOCKERS

None.

KNOWN REMAINING VERIFICATION

- Confirm CLIENT01 post-domain-join VM snapshot exists
- Verify Universal Forwarder configuration
- Verify Windows Event Log ingestion
- Perform basic Splunk searches
- Document telemetry pipeline
- Deploy Sysmon
- Verify Sysmon telemetry

END STATE FOR TONIGHT

The lab foundation is operational.

DC01 is healthy.
CLIENT01 is domain joined and healthy.
SPLUNK01 is operational.
Splunk Enterprise is running.
Splunk receiving is enabled on TCP 9997.
The Universal Forwarder is installed and running on CLIENT01.
CLIENT01 can reach SPLUNK01 on the receiving port.

The next session begins with verification of the actual Windows telemetry pipeline.
