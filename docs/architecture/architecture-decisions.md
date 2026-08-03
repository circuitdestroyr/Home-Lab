# Architecture Decisions

## Purpose

This document records major design decisions made during the development of the Cyber Enterprise Lab.

The goal is to maintain consistency and document the reasoning behind architectural choices.

---

# Decision 001 — Lab Focus

## Date

2026-08-03

## Decision

Build a cybersecurity-focused enterprise environment rather than a general-purpose IT homelab.

## Reason

The primary goal of this project is to develop practical skills in:

- Security operations
- Detection engineering
- Incident response
- Network security
- Active Directory security
- Purple team exercises

## Impact

All infrastructure decisions should support future cybersecurity scenarios, logging, monitoring, and investigations.

---

# Decision 002 — Host Distribution

## Date

2026-08-03

## Decision

Separate infrastructure workloads and security monitoring workloads between the available systems.

## Windows Laptop Responsibilities

- VMware environment
- Active Directory
- Windows endpoints
- Network appliances
- Infrastructure servers

## M2 Mac Responsibilities

- Splunk
- Security analysis tools
- Documentation
- Supporting security workloads

## Reason

Separating infrastructure and monitoring mirrors real-world environments where enterprise systems and security platforms are often managed independently.

---

# Decision 003 — Documentation Strategy

## Date

2026-08-03

## Decision

Use GitHub as the source of truth for the project.

## Reason

The repository will provide:

- Project history
- Architecture documentation
- Build records
- Security scenario documentation
- Portfolio visibility

## Impact

All major changes should include documentation updates.

---

# Decision 004 — Naming Convention

## Date

2026-08-03

## Decision

Use consistent enterprise-style naming conventions.

## Standards

| System Type | Naming Pattern | Example |
|---|---|---|
| Domain Controllers | DC## | DC01 |
| Clients | CLIENT## | CLIENT01 |
| Servers | SRV## | SRV01 |
| Security Tools | TOOL## | SPLUNK01 |
| Firewalls | FG## | FG01 |
| Network Devices | JNPR## | JNPR01 |

## Reason

Consistent naming makes the environment easier to manage and document.
