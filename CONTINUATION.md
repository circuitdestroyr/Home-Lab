Cyber Enterprise Lab — Continuation Statement

GitHub repository is the source of truth.

Current project phase:
Security Visibility Foundation

Current stopping point:
SPLUNK01 installation complete and operational.
Next major task is Windows telemetry collection from CLIENT01.

COMPLETED LAB FOUNDATION

DC01
- Windows Server 2022
- Active Directory Domain Services
- DNS
- homelab.local
- IP: 192.168.15.10
- Operational and verified

CLIENT01
- Windows 11 Pro
- IP: 192.168.15.20
- Joined homelab.local
- Domain authentication verified
- Secure channel verified
- AD computer object verified
- Post-domain-join VM snapshot still needs physical verification

SPLUNK01
- VMware VM on Windows laptop
- Ubuntu Server 24.04.4 LTS
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
- DC01 DNS forwarders configured:
  - 8.8.8.8
  - 8.8.4.4
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
- Splunk installation is operational

Installation verification:

    sudo /opt/splunk/bin/splunk status

Result:
    splunkd is running

Boot-start configuration:

    sudo /opt/splunk/bin/splunk enable boot-start -user splunk

Result:
    Init script installed at /etc/init.d/splunk.
    Init script is configured to run at boot.

DOCUMENTATION / GIT

Latest commit:
    c81a710 Document Splunk Enterprise installation

Commit pushed successfully to GitHub.

Current Git state:
    main is up to date with origin/main
    working tree clean

NEXT SESSION — START HERE

1. Verify CLIENT01 is powered on.
2. Verify CLIENT01 can communicate with DC01.
3. Confirm the CLIENT01 post-domain-join snapshot exists.
4. Decide and document the Windows telemetry architecture.
5. Configure Windows Event Log collection from CLIENT01 into SPLUNK01.
6. Verify events are arriving in Splunk.
7. Perform basic searches against the Windows data.
8. Document the telemetry configuration.
9. Commit and push documentation to GitHub.
10. After basic Windows Event Logs are working, move to Sysmon deployment.

IMPORTANT ARCHITECTURE RULE

Do not rebuild or move SPLUNK01.

SPLUNK01 belongs on the Windows laptop and is already operational.

NEXT MAJOR DATA FLOW

CLIENT01
    |
    | Windows Event Logs
    v
SPLUNK01
    |
    v
Splunk Search / Detection Engineering

Do not begin detection engineering until basic telemetry ingestion is verified.

WORKFLOW

Design → Document → Build → Verify → Commit

CURRENT BLOCKERS

None.

KNOWN REMAINING VERIFICATION

- Confirm CLIENT01 post-domain-join VM snapshot exists
- Configure Windows telemetry collection
- Verify Windows events are indexed by Splunk
- Configure Sysmon after basic Windows telemetry is working

SPLUNK TRIAL NOTE

Splunk Enterprise was installed on 2026-08-21.

The Enterprise Trial should be treated as time-limited and monitored during the project.

Do not change the license configuration now.

END STATE FOR TONIGHT

SPLUNK01 is installed, running, accessible through Splunk Web, configured for boot-start, and documented in GitHub.

The next session should begin with CLIENT01 → SPLUNK01 Windows telemetry.
