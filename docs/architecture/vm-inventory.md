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
| SPLUNK01 | SIEM / Log Analysis Platform | Linux | TBD | Planned |
| KALI01 | Security Testing Workstation | Kali Linux | TBD | Planned |

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
