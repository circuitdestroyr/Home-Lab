# Virtual Machine Inventory

## Purpose

This document tracks all virtual machines in the Cyber Enterprise Lab, including their purpose, operating system, network information, and current status.

---

## Production Environment

| Hostname | Purpose | Operating System | IP Address | Status |
|---|---|---|---|---|
| DC01 | Active Directory Domain Controller / DNS Server | Microsoft Windows Server 2022 Standard Evaluation | 192.168.15.10 | Operational |

---

## Endpoints

| Hostname | Purpose | Operating System | IP Address | Status |
|---|---|---|---|---|
| CLIENT01 | Standard Employee Workstation / User Endpoint | Windows 11 Pro | 192.168.15.20 | Operational - Domain Joined |

---

## Security Systems

| Hostname | Purpose | Operating System | IP Address | Status |
|---|---|---|---|---|
| SPLUNK01 | SIEM / Log Analysis Platform | Ubuntu Server 24.04 LTS | 192.168.15.30 | Operational - Base System |
| KALI01 | Security Testing Workstation | Kali Linux | TBD | Planned |

### SPLUNK01

Host Platform:

- Windows laptop
- VMware virtualization

Resources:

- 4 CPU cores
- 6 GB RAM
- 80 GB storage

Network:

- VMware NAT
- Static IP: 192.168.15.30
- Gateway: 192.168.15.2
- DNS: 192.168.15.10 (DC01)

Current Services:

- OpenSSH

Current Status:

- Ubuntu Server installed
- Static networking configured
- Gateway connectivity verified
- DC01 connectivity verified
- Internal DNS resolution verified
- External DNS resolution through DC01 verified
- SSH remote administration verified
- System updates completed
- Clean baseline VMware snapshot created
- Splunk Enterprise installation pending

---

## Network Infrastructure

| Hostname | Purpose | Platform | IP Address | Status |
|---|---|---|---|---|
| FG01 | Firewall / Security Gateway | FortiGate VM | TBD | Planned |
| JNPR01 | Routing / Switching Simulation | Juniper VM | TBD | Planned |

---

## Naming Convention

| Category | Convention | Example |
|---|---|---|
| Domain Controllers | DC## | DC01 |
| Clients | CLIENT## | CLIENT01 |
| Servers | SRV## | SRV01 |
| Security Tools | TOOL## | SPLUNK01 |
| Network Devices | Vendor + ## | FG01 / JNPR01 |
