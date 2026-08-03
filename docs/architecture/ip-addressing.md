# IP Addressing Plan

## Purpose

This document defines the network addressing strategy for the Cyber Enterprise Lab.

The goal is to maintain a realistic small business enterprise network design while supporting cybersecurity monitoring, attack simulation, and incident response exercises.

---

# Network Design

## Primary Lab Network

| Network | Purpose |
|---|---|
| TBD | Enterprise Internal Network |

---

# IP Allocation

| Device | Hostname | IP Address | Purpose |
|---|---|---|---|
| Domain Controller | DC01 | TBD | Active Directory / DNS |
| User Workstation | CLIENT01 | TBD | Employee Endpoint |
| SIEM Platform | SPLUNK01 | TBD | Security Monitoring |
| Security Testing System | KALI01 | TBD | Attack Simulation |
| Firewall | FG01 | TBD | Network Security Gateway |
| Network Device | JNPR01 | TBD | Routing / Switching |

---

# Future Network Segmentation

Planned network segments:

| Network | Purpose |
|---|---|
| Management | Network device administration |
| Users | Employee workstations |
| Servers | Infrastructure services |
| Security | Monitoring and analysis |
| Testing | Offensive security activities |

---

# Notes

The final addressing scheme will be selected before deploying additional systems to maintain consistency throughout the lab.

All future systems will be documented before deployment.
