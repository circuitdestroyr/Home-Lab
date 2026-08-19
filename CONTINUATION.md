# Cyber Enterprise Lab — Continuation Statement

GitHub repository is the source of truth.

Current project phase:
Security Visibility Foundation

Current stopping point:
SPLUNK01

Completed foundation:

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
- Post-domain-join snapshot still needs physical verification

SPLUNK01
- VMware VM on Windows laptop
- Ubuntu Server 24.04 LTS
- 4 vCPU
- 6 GB RAM
- 80 GB storage
- OpenSSH installed
- Static IP: 192.168.15.30
- Gateway: 192.168.15.2
- DNS: 192.168.15.10
- VMware NAT
- Gateway connectivity verified
- DC01 connectivity verified
- dc01.homelab.local resolution verified
- SSH remote administration verified
- Ubuntu system updates completed
- Clean SPLUNK01 baseline VMware snapshot created

DNS troubleshooting completed:

Problem:
- SPLUNK01 could resolve some public domains
- splunk.com returned SERVFAIL through DC01
- download.splunk.com returned SERVFAIL through DC01
- Direct queries to public DNS such as 8.8.8.8 worked
- DC01 DNS service was running
- DNS recursion was enabled
- Root hints were present
- Direct queries to multiple root servers timed out
- DC01 successfully queried 8.8.8.8 directly

Resolution:
- Added DC01 DNS forwarders:
  - 8.8.8.8
  - 8.8.4.4
- Verified DC01 successfully resolves:
  - splunk.com
  - download.splunk.com
- SPLUNK01 continues to use DC01 (192.168.15.10) as its DNS server
- No public DNS servers were configured directly on SPLUNK01

Documentation completed:
- docs/build-log.md updated with Session 6 DNS troubleshooting
- docs/project-status.md updated with current SPLUNK01 state
- docs/architecture/architecture-decisions.md reflects SPLUNK01 on Windows laptop

Important architecture decision:
Decision 002 is already correct.
SPLUNK01 belongs on the Windows laptop.
Do not move or rebuild SPLUNK01.

Current SPLUNK01 status:
- Splunk Enterprise NOT installed yet
- Windows telemetry NOT configured yet
- DNS troubleshooting is complete

NEXT SESSION — START HERE:

1. SSH into SPLUNK01 from the Windows laptop.
2. Verify external DNS from SPLUNK01:

   resolvectl query download.splunk.com

3. If DNS resolves, retry the Splunk Enterprise download.
4. Install the Splunk .deb package.
5. Complete initial Splunk configuration.
6. Start Splunk and verify the service.
7. Verify Splunk Web interface.
8. Confirm Splunk starts successfully.
9. Document and verify the completed SPLUNK01 installation.
10. Only then move into Windows telemetry collection.

Do NOT repeat today's DNS troubleshooting unless the SPLUNK01 DNS test fails.

Workflow:
Design → Document → Build → Verify → Commit

Last documentation checkpoint:
- Build log Session 6 completed
- Project status updated

Suggested next commit after the Splunk installation is complete:

Install and configure SPLUNK01
