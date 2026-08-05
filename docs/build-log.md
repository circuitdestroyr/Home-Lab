# Build Log

## Session 1

Date: 2026-08-03

## Completed

- Created GitHub repository
- Created initial README
- Created project documentation structure
- Created project tracking files:
  - project-status.md
  - roadmap.md
  - build-log.md

## Environment Status

- DC01 VM created
- Active Directory deployment pending

## Next Steps

- Configure DC01 networking
- Assign static IP
- Install Active Directory Domain Services
- Promote DC01

# Session 2— DC01 Health Verification

## Objective

Verify that the Active Directory Domain Controller (DC01) is healthy before introducing the first domain-joined workstation (CLIENT01).

The goal was to establish a known-good baseline before expanding the environment.

---

# Verification Tests

## Test 1 — Verify Active Directory Shares

### Command

```cmd
net share
```

### Purpose

Verify that Active Directory created the required domain shares.

The two important shares are:

- NETLOGON — Used for domain logon scripts and client authentication processes.
- SYSVOL — Stores Group Policy Objects (GPOs) and other Active Directory related files.

### Output

```text
NETLOGON     C:\Windows\SYSVOL\sysvol\homelab.local\SCRIPTS
SYSVOL       C:\Windows\SYSVOL\sysvol
```

### Analysis

The presence of both SYSVOL and NETLOGON confirms that Active Directory Domain Services successfully created the required shares.

### Result

PASS ✅

---

## Test 2 — Verify DNS Resolution

### Command

```cmd
nslookup homelab.local
```

### Purpose

Verify that the Active Directory DNS service can resolve the domain name.

### Output

```text
Name: homelab.local
Address: 192.168.15.10
```

### Analysis

The domain successfully resolves to the DC01 IP address.

A timeout was observed when querying the IPv6 loopback address (::1), but the domain resolution completed successfully.

### Result

PASS ✅

---

## Test 3 — Verify Domain Controller Advertising

### Command

```cmd
dcdiag /test:Advertising
```

### Purpose

Verify that DC01 is correctly advertising itself as an Active Directory Domain Controller.

### Output

```text
DC01 passed test Connectivity

DC01 passed test Advertising
```

### Analysis

DC01 successfully passed the advertising test and is available as a domain controller.

### Result

PASS ✅

---

## Test 4 — Verify Windows Time Service

### Command

```cmd
w32tm /query /status
```

### Purpose

Verify that the Windows Time service is functioning.

Time synchronization is critical for Active Directory authentication because Kerberos relies on accurate system time.

### Output

```text
Source: Local CMOS Clock
```

### Analysis

DC01 is currently acting as the authoritative time source for this single-domain-controller lab environment.

Future configuration may include external NTP synchronization.

### Result

PASS ✅

---

# Conclusion

DC01 successfully passed all baseline health verification tests.

The Active Directory environment is ready for expansion.

---

# Next Steps

- Update project status
- Deploy CLIENT01
- Configure CLIENT01 networking
- Join CLIENT01 to homelab.local

# Session 3 — CLIENT01 Deployment

## Objective

Deploy the first Windows endpoint for the Cyber Enterprise Lab.

CLIENT01 provides a realistic employee workstation platform for:

- Active Directory authentication
- Security logging
- Detection engineering
- Incident response scenarios

---

## Virtual Machine Deployment

CLIENT01 was created in VMware Workstation 17.5.

Configuration:

| Component | Value |
|---|---|
| Hostname | CLIENT01 |
| Operating System | Windows 11 Pro |
| CPU | 2 cores |
| Memory | 4 GB RAM |
| Storage | 64 GB |
| Disk Configuration | Single virtual disk |
| Network | VMware NAT |

---

## Windows Installation

Completed:

- Windows 11 Pro installation completed
- Device hostname configured as CLIENT01
- Work/school setup selected
- Domain join deferred until post-install configuration
- Local administrator account created

---

## Current Status

CLIENT01 is operational and ready for Active Directory integration.

Pending:

- Verify hostname
- Verify network configuration
- Configure DNS pointing to DC01
- Join homelab.local domain
- Verify domain authentication

---

## Next Steps

- Complete CLIENT01 baseline verification
- Configure Active Directory domain membership
- Begin endpoint security configuration
