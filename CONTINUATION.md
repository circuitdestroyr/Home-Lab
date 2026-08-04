Cyber Enterprise Lab Continuation Brief

The GitHub repository is the source of truth for this project.

Before making architecture changes, recommendations, or adding new documentation:
Review the existing repository structure and respect decisions already documented.

Primary architecture documents:
- docs/architecture/architecture-decisions.md
- docs/architecture/vm-inventory.md
- docs/architecture/active-directory-design.md

Project tracking:
- docs/project-status.md
- docs/roadmap.md
- docs/build-log.md

Project Goal:

Build a cybersecurity-focused enterprise lab designed for:
- Security operations
- Detection engineering
- Incident response
- Active Directory security
- Network security
- Purple team exercises

The lab is not intended to be a generic IT homelab. All infrastructure decisions should support future security scenarios, logging, monitoring, investigations, and attack simulations.

Current Architecture Decisions:

Decision 001 — Lab Focus:
The environment is designed as a cybersecurity enterprise environment.

Decision 002 — Host Distribution:
Workloads are distributed between available physical systems.

Windows Laptop responsibilities:
- VMware environment
- Active Directory
- Windows endpoints
- Infrastructure servers
- Network appliance simulations

M2 Mac responsibilities:
- Splunk
- Security analysis tools
- Linux security workloads
- Supporting security tools

Reason:
Separate infrastructure workloads from security monitoring workloads while respecting available hardware resources.

Decision 003 — Documentation Strategy:
GitHub is the source of truth.

All major changes should follow:
Design → Document → Build → Verify → Commit

Decision 004 — Naming Convention:

Domain Controllers:
DC##

Clients:
CLIENT##

Servers:
SRV##

Security Tools:
TOOL##

Firewalls:
FG##

Network Devices:
JNPR##

Completed Milestone:

DC01 Foundation is complete.

Completed:
- Windows Server 2022 installed
- DC01 deployed
- Static IP configured
- Active Directory Domain Services installed
- Domain created
- DNS configured
- VMware Tools installed
- SYSVOL verified
- NETLOGON verified
- DNS resolution tested
- Domain Controller Advertising verified
- Windows Time service verified

Current Environment:

Domain:
homelab.local

Domain Controller:

Hostname:
DC01

Operating System:
Microsoft Windows Server 2022 Standard Evaluation

Role:
Active Directory Domain Controller / DNS Server

IP:
192.168.15.10

Resources:
- 2 CPU cores
- 4 GB RAM
- 60 GB storage

Current Project Phase:

Preparing CLIENT01 deployment.

CLIENT01 Design:

Hostname:
CLIENT01

Role:
Standard Employee Workstation / User Endpoint

Operating System:
Windows 11 Pro

Planned Resources:
- 2 CPU cores
- 4 GB RAM
- 64 GB storage

Purpose:
Provide a realistic employee endpoint for:
- Authentication events
- Security logging
- Detection engineering
- Incident response scenarios

Future Planned Systems:

SPLUNK01:
SIEM / log analysis platform

KALI01:
Security testing workstation

FG01:
Firewall/security gateway simulation

JNPR01:
Routing/switching simulation

Important Workflow Rule:

Do not create duplicate documentation if a decision already exists.

Before adding new files:
Check existing architecture documents.

Documentation standards:

Build Log:
Documents what was done, commands used, purpose, output, analysis, and verification.

Project Status:
Shows current progress.

Architecture Decisions:
Documents why decisions were made.

VM Inventory:
Tracks systems and their current status.

Current Next Steps:

1. Finish architecture documentation updates.
2. Commit CLIENT01 role definition.
3. Review repository state.
4. Build CLIENT01.
5. Configure CLIENT01 networking.
6. Point CLIENT01 DNS to DC01.
7. Join CLIENT01 to homelab.local.
8. Verify domain authentication.
