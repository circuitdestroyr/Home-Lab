Cyber Enterprise Lab — Continuation Statement

Repository:
GitHub repository is the source of truth.

Repository state:
- Branch: main
- Working tree: clean
- Latest local/remote commit: ecfbbc1
- Commit: Update project status for Windows telemetry
- Changes successfully pushed to GitHub

CURRENT PROJECT PHASE

Security Visibility Foundation

CURRENT LAB STATE

DC01
- Windows Server 2022
- Active Directory Domain Services operational
- DNS operational
- Domain: homelab.local
- IP: 192.168.15.10
- SYSVOL verified
- NETLOGON verified
- Domain Controller health checks completed
- External DNS forwarders configured
- External DNS resolution verified

CLIENT01
- Windows 11 Pro
- IP: 192.168.15.20
- Domain joined to homelab.local
- DNS points to DC01
- Domain authentication verified
- Secure channel verified
- Active Directory computer object verified
- TCP connectivity to SPLUNK01 verified
- TCP 8089 connectivity verified
- TCP 9997 connectivity verified
- Splunk Universal Forwarder 10.4.2 installed
- Universal Forwarder service running
- Forwarding to SPLUNK01 configured
- Application Event Log collection configured
- Security Event Log collection configured
- System Event Log collection configured

SPLUNK01
- Ubuntu Server 24.04 LTS
- IP: 192.168.15.30
- Gateway: 192.168.15.2
- DNS: 192.168.15.10
- VMware NAT
- 4 vCPU
- 6 GB RAM
- 80 GB storage
- OpenSSH installed
- SSH remote administration verified
- System updates completed
- Clean baseline VMware snapshot created
- Splunk Enterprise 10.4.2 installed
- Splunk administrator account created
- Splunk Web verified on port 8000
- Splunk management port verified on 8089
- Splunk service verified running
- Splunk configured for boot-start
- Splunk receiving configured on TCP 9997

VERIFIED WINDOWS TELEMETRY PIPELINE

CLIENT01
→ Windows Event Logs
→ Splunk Universal Forwarder
→ TCP 9997
→ SPLUNK01
→ Splunk Enterprise
→ main index
→ Splunk Search

Verified:
- Application Event Log ingestion
- Security Event Log ingestion
- System Event Log ingestion
- Splunk indexing
- CLIENT01 events searchable in Splunk
- Active forwarding to SPLUNK01

Verified telemetry counts from the lab documentation:
- Application: 18 events
- Security: 397 events
- System: 19 events

Verified test event:
- Host: CLIENT01
- Source: WinEventLog:Application
- Sourcetype: WinEventLog:Application
- Index: main
- Event source: CyberLab
- Event ID: 1000

CURRENT SECURITY OPERATIONS STATE

Completed:
- SPLUNK01 security monitoring foundation
- Splunk Enterprise installation
- Splunk receiving configuration
- CLIENT01 Universal Forwarder installation
- Windows Application/Security/System telemetry collection
- Windows telemetry ingestion verification
- Basic Splunk searches
- Windows telemetry pipeline documentation

NOT YET COMPLETED

- CLIENT01 post-domain-join VMware snapshot verification
- Sysmon deployment
- Sysmon configuration
- Sysmon service verification
- Sysmon event generation verification
- Sysmon events in Splunk verification
- Sysmon telemetry documentation
- Detection engineering
- Security alert creation and tuning
- Additional telemetry sources
- Linux log collection
- Firewall log collection
- Network infrastructure telemetry

NEXT SESSION — START HERE

1. Verify whether a current CLIENT01 VMware snapshot exists after the domain join.
2. If appropriate, create a clearly named pre-Sysmon snapshot.
3. Deploy Sysmon on CLIENT01.
4. Configure Sysmon security telemetry.
5. Verify the Sysmon service is running.
6. Generate/observe Sysmon events locally on CLIENT01.
7. Verify Sysmon events are arriving in Splunk.
8. Confirm the Sysmon sourcetype/index and searchable fields.
9. Verify Sysmon Event ID 1 (Process Create).
10. Document the verified Sysmon telemetry pipeline.
11. Commit documentation changes.
12. Push changes to GitHub.
13. Begin detection engineering only after telemetry is verified.

IMPORTANT WORKFLOW

Do not rebuild DC01.
Do not rebuild CLIENT01.
Do not rebuild SPLUNK01.
Do not change the existing DNS architecture.
Do not change the existing VMware network architecture unless a specific problem requires it.

Use:

Design → Document → Build → Verify → Commit → Push

CURRENT BLOCKERS

None.

TONIGHT'S STOPPING POINT

The Windows telemetry foundation is complete and documented.

GitHub is synchronized.

The repository is clean.

No further work is required tonight.

NEXT MAJOR MILESTONE

Deploy and verify Sysmon on CLIENT01, then begin detection engineering using verified Windows and Sysmon telemetry.
