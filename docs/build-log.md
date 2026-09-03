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

# Session 5 — SPLUNK01 Initial Deployment

## Objective

Deploy the initial SIEM/security monitoring server for the Security Visibility Foundation phase.

SPLUNK01 will provide the platform for:

- Splunk Enterprise
- Windows event collection
- Security monitoring
- Detection engineering
- Incident investigation

---

## Virtual Machine Deployment

SPLUNK01 was created in VMware Workstation.

Configuration:

| Component | Value |
|---|---|
| Hostname | SPLUNK01 |
| Operating System | Ubuntu Server 24.04 LTS |
| CPU | 4 vCPU |
| Memory | 6 GB RAM |
| Storage | 80 GB |
| Network | VMware NAT |
| IP Address | 192.168.15.30 |
| Gateway | 192.168.15.2 |
| DNS Server | 192.168.15.10 |

---

## Ubuntu Installation

Completed:

- Ubuntu Server 24.04 LTS installed
- OpenSSH server installed
- Initial DHCP networking verified
- Static network configuration applied

---

## Network Configuration

SPLUNK01 initially received DHCP address `192.168.15.130`.

Netplan was subsequently configured with the planned static address:

`192.168.15.30/24`

DNS was changed from the VMware-provided DNS service (`192.168.15.2`) to DC01 (`192.168.15.10`) so that SPLUNK01 uses the lab's Active Directory DNS infrastructure.

---

## Network Verification

Verified:

- Gateway connectivity to `192.168.15.2`
- Connectivity to DC01 at `192.168.15.10`
- DNS resolution of `dc01.homelab.local`
- SSH remote administration using `192.168.15.30`

### Result

Network configuration: **PASS**

---

## Current Status

SPLUNK01 is installed and network configuration is complete.

Completed:

- VMware VM created
- Ubuntu Server 24.04 LTS installed
- OpenSSH server installed
- Static IP configured
- Gateway connectivity verified
- DC01 connectivity verified
- Active Directory DNS resolution verified
- SSH remote administration verified
- Ubuntu system update started

Pending:

- Complete Ubuntu system updates
- Verify SPLUNK01 OS baseline
- Verify SSH after system updates
- Create clean SPLUNK01 OS baseline snapshot
- Install Splunk Enterprise
- Configure Windows telemetry collection

---

## Next Steps

- Complete SPLUNK01 OS verification
- Create clean OS baseline snapshot
- Install Splunk Enterprise
- Begin Windows telemetry collection

# Session 6 — SPLUNK01 DNS Troubleshooting

---

## Objective

Resolve and document an external DNS resolution issue encountered while preparing SPLUNK01 for Splunk Enterprise installation.

SPLUNK01 was correctly configured to use DC01 (`192.168.15.10`) as its DNS server, but external Splunk domains were returning `SERVFAIL`.

The goal was to identify the cause without bypassing the lab's Active Directory DNS architecture.

---

## Initial DNS Issue

SPLUNK01 was unable to resolve:

- `splunk.com`
- `download.splunk.com`

Both returned DNS `SERVFAIL` responses when queried through DC01.

General Internet DNS resolution was still functioning for other domains.

---

## DNS Troubleshooting

### Test 1 — Verify External DNS Resolution

### Command

`resolvectl query google.com`

### Result

PASS

Google DNS records resolved successfully through the configured DNS path.

---

### Test 2 — Verify External DNS Resolution Through DC01

### Command

`nslookup facebook.com 192.168.15.10`

### Result

PASS

Facebook successfully resolved through DC01.

This confirmed that DC01 was providing functional external DNS resolution for some public domains.

---

### Test 3 — Test Splunk DNS Resolution Through DC01

### Command

`nslookup splunk.com 192.168.15.10`

### Result

FAIL

The query returned:

`SERVFAIL`

The Splunk download hostname produced the same result.

### Command

`nslookup download.splunk.com 192.168.15.10`

### Result

FAIL

The query returned:

`SERVFAIL`

---

### Test 4 — Test Splunk DNS Resolution Through Public DNS

### Command

`nslookup splunk.com 8.8.8.8`

### Result

PASS

`8.8.8.8` successfully resolved `splunk.com`.

---

### Test 5 — Test Splunk Download DNS Resolution

### Command

`nslookup download.splunk.com 8.8.8.8`

### Result

PASS

The hostname successfully resolved to CloudFront addresses.

---

## DC01 DNS Investigation

The DNS Server service was verified as running.

### Command

`Get-Service DNS`

### Result

PASS

The DNS Server service was running on DC01.

---

### DNS Recursion

### Command

`Get-DnsServerRecursion`

### Result

PASS

DNS recursion was enabled.

---

### Root Hint Verification

### Command

`Get-DnsServerRootHint`

### Result

PASS

Standard DNS root server entries were present.

Direct DNS queries to multiple root servers timed out, while DC01 was able to successfully query `8.8.8.8` directly.

This indicated that the root-hint resolution path was not functioning correctly in the current lab network environment.

---

## DNS Forwarder Configuration

To provide a reliable external DNS resolution path while maintaining DC01 as the DNS server for the lab, DNS forwarders were configured on DC01.

### Command

`Add-DnsServerForwarder -IPAddress 8.8.8.8,8.8.4.4`

Configured forwarders:

- `8.8.8.8`
- `8.8.4.4`

### Verification

`Get-DnsServerForwarder`

### Result

PASS

Configured forwarders were successfully displayed.

---

## Post-Configuration Verification

### Command

`Resolve-DnsName splunk.com`

### Result

PASS

DC01 successfully resolved `splunk.com`.

### Command

`Resolve-DnsName download.splunk.com`

### Result

PASS

DC01 successfully resolved `download.splunk.com` and its CloudFront destination.

---

## Architecture Result

SPLUNK01 continues to use DC01 as its DNS server:

`192.168.15.10`

External DNS resolution is handled by DC01 using the configured DNS forwarders.

No public DNS servers were configured directly on SPLUNK01.

The Active Directory DNS architecture remains intact, with DC01 providing internal DNS resolution and handling external DNS resolution on behalf of lab systems.

---

## Result

DNS troubleshooting: **COMPLETE**

DC01 external DNS resolution: **PASS**

SPLUNK01 DNS configuration: **PASS**

Splunk download domain resolution through DC01: **PASS**

Splunk Enterprise installation: **PENDING**

---

## Next Steps

- Verify external DNS resolution from SPLUNK01
- Download Splunk Enterprise
- Install Splunk Enterprise
- Start and verify Splunk services
- Verify Splunk Web interface
- Begin Windows telemetry collection

# Session 7 — CLIENT01 Telemetry Preparation

## CLIENT01 Domain Verification

Verified CLIENT01 connectivity and domain functionality.

Tests performed:

- `nslookup dc01.homelab.local`
  - Resolved to `192.168.15.10`
- `nslookup -type=SRV _ldap._tcp.dc._msdcs.homelab.local`
  - LDAP SRV record resolved successfully
  - Target: `dc01.homelab.local`
  - Port: `389`
- `Test-ComputerSecureChannel`
  - Result: `True`
- `nltest /dsgetdc:homelab.local`
  - Successfully located `DC01.homelab.local`
  - Address: `192.168.15.10`

## CLIENT01 → SPLUNK01 Connectivity

Verified connectivity from CLIENT01 to SPLUNK01:

- SPLUNK01 IP: `192.168.15.30`
- ICMP ping: successful, 0% packet loss
- TCP `8089`: successful
- TCP `9997`: successful

## SPLUNK01 Receiving Configuration

Splunk Enterprise on SPLUNK01 was configured with receiving enabled on TCP port `9997`.

CLIENT01 successfully established TCP connectivity to:

`192.168.15.30:9997`

## Splunk Universal Forwarder Installation

Installed Splunk Universal Forwarder `10.4.2` on CLIENT01.

Selected configuration:

- Deployment type: On-premises
- Installation path: Default
- Service account: Local System
- SeBackupPrivilege: enabled
- SeSecurityPrivilege: enabled
- Performance Monitor Users: enabled
- Windows Event Logs:
  - Application
  - Security
  - System
- Performance Monitor collection: not enabled
- Deployment Server: not configured
- Receiving Indexer: `192.168.15.30:9997`
- UF administrator username: `ufadmin`

## Universal Forwarder Verification

Verified the Windows service on CLIENT01:

```powershell
Get-Service Result:

SplunkForwarder — Running
```

Current Stopping Point

Universal Forwarder installation is complete and the service is running.

Windows Event Log ingestion into Splunk has not yet been verified.

# Next Step

Verify Universal Forwarder configuration and confirm that CLIENT01 Windows Event Logs are being indexed by SPLUNK01.

## Session 8 — Windows Telemetry Pipeline Verification

### Objective

Verify that Windows Event Logs generated on CLIENT01 are successfully forwarded by the Splunk Universal Forwarder to SPLUNK01 and indexed by Splunk Enterprise.

### Verification Performed

CLIENT01:

- `SplunkForwarder` Windows service verified as Running.
- Universal Forwarder forwarding destination verified as `192.168.15.30:9997`.
- Forwarding initially showed as inactive because SPLUNK01 was powered off.
- After SPLUNK01 was powered on and `splunkd` was confirmed running, the forwarder reported `192.168.15.30:9997` as an active forward.
- SPLUNK01 confirmed listening on TCP 9997.
- A controlled Application event was generated using the `CyberLab` source.
- Event ID: `1000`.
- Test message: `Cyber Enterprise Lab telemetry test - CLIENT01`.
- The event was verified locally on CLIENT01.

### Splunk Verification

The test event was successfully located in Splunk.

Verified event metadata:

- Host: `CLIENT01`
- Source: `WinEventLog:Application`
- Sourcetype: `WinEventLog:Application`
- Index: `main`

Additional telemetry verification confirmed events from all three configured Windows Event Log channels:

| Windows Log | Source | Count Observed |
|---|---|---:|
| Application | `WinEventLog:Application` | 18 |
| Security | `WinEventLog:Security` | 397 |
| System | `WinEventLog:System` | 19 |

### Result

The basic Windows telemetry pipeline is VERIFIED:

`CLIENT01 → Windows Event Logs → Splunk Universal Forwarder → TCP 9997 → SPLUNK01 → Splunk main index → Search`

### Next Session

- Verify/create CLIENT01 pre-Sysmon VMware snapshot.
- Deploy Microsoft Sysmon.
- Configure Sysmon security telemetry.
- Verify Sysmon locally.
- Verify Sysmon events in Splunk.
- Document and commit the Sysmon telemetry milestone.

Detection engineering has not yet started.
