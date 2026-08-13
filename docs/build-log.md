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

CLIENT01 is operational and successfully integrated with Active Directory.

Completed:

- Verified hostname
- Verified network configuration
- Configured DNS pointing to DC01
- Joined homelab.local domain
- Verified domain authentication

## Active Directory Integration

Completed:

- Verified CLIENT01 network connectivity to DC01
- Verified Active Directory DNS resolution
- Verified domain controller discovery
- Joined CLIENT01 to homelab.local
- Verified domain authentication
- Verified secure channel communication

---

## Next Steps

- Complete CLIENT01 baseline verification
- Verify post-domain-join VM snapshot
- Begin endpoint security configuration

---

# Session 3 — CLIENT01 Active Directory Integration

## Objective

Complete the integration of CLIENT01 into the homelab.local Active Directory environment.

The goal was to establish a functioning enterprise workstation relationship with DC01 and verify:

- Active Directory domain membership
- DNS-based domain discovery
- Domain authentication
- Secure channel communication

---

## Network Configuration

CLIENT01 was connected to the VMware NAT network alongside DC01.

Configuration:

| Component | Value |
| --------- | ----- |
| Network | VMware NAT |
| Domain Controller | DC01 |
| DNS Server | 192.168.15.10 |
| Domain | homelab.local |

---

## Active Directory Discovery Verification

### Test 1 — Verify Connectivity to DC01

### Command

```powershell
ping 192.168.15.10
```

### Purpose

Verify that CLIENT01 can communicate with DC01 over the lab network.

### Result

PASS

---

## Test 2 — Verify Domain Discovery

### Command

```powershell
nltest /dsgetdc:homelab.local
```

### Purpose

Verify that CLIENT01 can locate the Active Directory Domain Controller for homelab.local.

### Result

PASS

---

## Test 3 — Verify Domain Membership

### Command

```powershell
systeminfo | findstr /B /C:"Domain"
```

### Output

```text
Domain: homelab.local
```

### Result

PASS

---

## Test 4 — Verify Domain Authentication

### Command

```powershell
whoami
```

### Output

```text
homelab\administrator
```

### Result

PASS

---

## Test 5 — Verify Secure Channel

### Command

```powershell
Test-ComputerSecureChannel
```

### Output

```text
True
```

### Result

PASS

---

## Test 6 — Verify Active Directory Computer Object

CLIENT01 was verified in Active Directory under:

```text
homelab.local
└── Computers
    └── CLIENT01
```

### Result

PASS

---

## CLIENT01 Integration Conclusion

CLIENT01 successfully completed Active Directory integration.

Verified:

- Network connectivity to DC01
- DNS-based domain discovery
- Active Directory domain membership
- Domain authentication
- Secure channel communication
- Active Directory computer object creation

CLIENT01 is now operational as a domain-joined enterprise workstation.

---

# Session 4 — CLIENT01 Documentation Reconciliation

## Objective

Reconcile project status documentation with the completed CLIENT01 Active Directory integration.

## Completed Verification

CLIENT01 Active Directory integration has been completed and verified.

Verified:

- CLIENT01 DNS configured to use DC01
- Active Directory discovery successful
- CLIENT01 joined to `homelab.local`
- Domain authentication successful
- Secure channel verification successful
- CLIENT01 computer object confirmed in Active Directory

## Documentation Update

The project status documentation previously listed CLIENT01 Active Directory integration tasks as pending.

Those tasks have now been updated to reflect their verified completion.

CLIENT01 status:

**Operational — Domain Joined**

## Snapshot Verification

A post-domain-join VM snapshot is intended to serve as the CLIENT01 baseline.

The existence of this snapshot still requires physical verification in VMware.

Status:

**Pending verification**

The snapshot will not be considered complete until it has been verified.

## Result

CLIENT01 Active Directory integration: **COMPLETE**

Post-domain-join snapshot: **PENDING VERIFICATION**

## Next Step

Verify the CLIENT01 post-domain-join snapshot before beginning Security Visibility Foundation work and SPLUNK01 design.
