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

The lab is not intended to be a generic IT homelab.

All infrastructure decisions should support future security scenarios, logging, monitoring, investigations, and attack simulations.


Current Architecture Decisions:

Decision 001 — Lab Focus

The environment is designed as a cybersecurity enterprise environment.

Primary objectives:

- Security operations practice
- Detection engineering
- Incident response workflows
- Active Directory security
- Network security
- Purple team exercises


Decision 002 — Host Distribution

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


Decision 003 — Documentation Strategy

GitHub is the source of truth.

All major changes should follow:

Design → Document → Build → Verify → Commit


Decision 004 — Naming Convention

Enterprise-style naming conventions are used.

Standards:

Domain Controllers:
DC##

Example:
DC01

Clients:
CLIENT##

Example:
CLIENT01

Servers:
SRV##

Example:
SRV01

Security Tools:
TOOL##

Example:
SPLUNK01

Firewalls:
FG##

Example:
FG01

Network Devices:
JNPR##

Example:
JNPR01


Completed Milestones:

## DC01 Foundation

Status:
Complete

DC01:

Hostname:
DC01

Operating System:
Microsoft Windows Server 2022 Standard Evaluation

Role:
Active Directory Domain Controller / DNS Server

Domain:
homelab.local

IP:
192.168.15.10

Resources:

- 2 CPU cores
- 4 GB RAM
- 60 GB storage


Completed DC01 tasks:

- Windows Server installation
- Static IP configuration
- Active Directory Domain Services installation
- Domain Controller promotion
- DNS configuration
- VMware Tools installation
- SYSVOL verification
- NETLOGON verification
- DNS resolution verification
- Domain Controller Advertising verification
- Windows Time verification


## CLIENT01 Deployment

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


Current Environment:

Domain:

homelab.local


Domain Controller:

DC01

Services:

- Active Directory Domain Services
- DNS
- Kerberos
- Domain authentication


Domain Endpoint:

CLIENT01

Services:

- Windows 11 enterprise workstation
- Domain authentication endpoint
- Future security telemetry source


Current Project Phase:

Security Visibility Foundation


Next Planned Systems:

SPLUNK01

Role:
SIEM / log analysis platform

Planned responsibilities:

- Collect Windows event logs
- Analyze authentication activity
- Build detections
- Support investigations


KALI01

Role:
Security testing workstation

Purpose:

- Controlled attack simulations
- Security testing
- Purple team exercises


FG01

Role:
Firewall/security gateway simulation


JNPR01

Role:
Routing/switching simulation


Next Steps:

1. Review repository state.
2. Update documentation files:
   - docs/build-log.md
   - docs/project-status.md
   - docs/architecture/vm-inventory.md

3. Commit CLIENT01 completion changes.

4. Begin Security Visibility Foundation planning.

5. Design SPLUNK01 deployment.

6. Plan Windows telemetry collection from:
   - DC01
   - CLIENT01


Important Workflow Rule:

Do not create duplicate documentation if a decision already exists.

Before adding new files:
Check existing architecture documents.


Current Lab State:

The lab has moved from infrastructure deployment into security visibility preparation.

Current foundation:

DC01
+
CLIENT01
+
Active Directory
+
Domain Authentication

Next objective:

Build the monitoring and detection layer.
