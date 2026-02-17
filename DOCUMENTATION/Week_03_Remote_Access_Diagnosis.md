# Week_03 — Remote Access & Infrastructure Diagnosis

---

## Overview

This document provides a complete technical breakdown of all commands executed during remote validation of the ECRL Splunk VM (`10.11.20.205`) from an off-campus location via Marist VPN.

### Objectives

- Validate remote connectivity  
- Confirm service availability  
- Diagnose xRDP session failures  
- Investigate Splunk service status  
- Identify root cause of infrastructure malfunction  

---

# Phase 1 — VPN & Network Validation (Windows Host)

---

## 1️⃣ Verify VPN IP Assignment

```powershell
ipconfig
```

### Purpose
Confirm Cisco Secure Client assigned an internal Marist VPN address.

### Expected
- IP in the `10.6.x.x` range

### Result
- VPN adapter assigned `10.6.x.x`

### Conclusion
Layer 3 connectivity to the internal Marist network successfully established.

---

## 2️⃣ Validate Route Injection

```powershell
route print
```

### Purpose
Confirm internal network routes (`10.0.0.0/8`) were injected into the routing table.

### Expected
- Route to `10.0.0.0/8` via Cisco AnyConnect adapter

### Result
- Route present

### Conclusion
Traffic destined for ECRL subnet (`10.11.20.0/24`) traverses VPN tunnel correctly.

---

## 3️⃣ Test Network Reachability to SOC Subnet

```powershell
ping 10.11.20.205
ping 10.11.20.206
ping 10.11.20.207
```

### Purpose
Verify host availability at Layer 3.

### Result
- All three IP addresses responded successfully.

### Conclusion
All VMs are powered on and reachable at the network level.

---

## 4️⃣ Validate Service Ports (Windows Host)

```powershell
Test-NetConnection 10.11.20.205 -Port 3389
Test-NetConnection 10.11.20.205 -Port 22
Test-NetConnection 10.11.20.205 -Port 8000
```

### Purpose
Verify:

- RDP availability (3389)
- SSH availability (22)
- Splunk Web availability (8000)

### Results

- Port 3389 → `True`
- Port 22 → `True`
- Port 8000 → `False`

### Conclusion

- xRDP listening
- SSH available
- Splunk Web not running or not listening

---

# Phase 2 — SSH Session Validation

---

## 5️⃣ Establish SSH Session

```powershell
ssh splunkcapping@10.11.20.205
```

### Purpose
Obtain shell access to Splunk VM for deeper inspection.

### Result
- Authentication successful
- Interactive shell established

### Conclusion

- SSH service functional
- Credentials valid
- VM responsive

---

# Phase 3 — xRDP Service Validation

---

## 6️⃣ Confirm xRDP Listening

```bash
sudo ss -lntp | grep 3389
```

### Purpose
Confirm xRDP is actively listening on TCP/3389.

### Result

```
LISTEN *:3389 users:(("xrdp",pid=1192))
```

### Conclusion

- RDP service is running
- Teal screen not caused by network-level failure

---

# Phase 4 — Splunk Service Investigation

---

## 7️⃣ Check Splunk Status

```bash
sudo /opt/splunk/bin/splunk status
```

### Purpose
Determine operational state of Splunk daemon.

### Result

- `splunkd` not running
- Stale PID file present
- PID removal failed due to read-only filesystem

### Conclusion
Splunk cannot start because filesystem does not allow write operations.

---

# Phase 5 — Filesystem Integrity Investigation

---

## 8️⃣ Check Root Mount Status

```bash
mount | grep " on / "
```

### Result

```
/dev/sda2 on / type ext4 (rw,relatime,emergency_ro)
```

### Purpose
Identify mount flags for root filesystem.

### Interpretation

- Filesystem type: `ext4`
- Device: `/dev/sda2`
- Flag: `emergency_ro`

### Meaning
Kernel placed filesystem into emergency read-only mode due to detected integrity error.

---

## 9️⃣ Verify Write Capability

```bash
touch /tmp/testfile && echo "TMP_OK" || echo "TMP_FAIL"
```

### Result

```
TMP_FAIL
Read-only file system
```

### Conclusion
System-wide writes blocked.  
Confirms filesystem is locked.

---

## 🔟 Identify Root Device

```bash
findmnt -no SOURCE /
```

### Result

```
/dev/sda2
```

### Purpose
Identify underlying block device for root filesystem.

### Conclusion
Root filesystem resides on `/dev/sda2`.  
Required for `fsck` or snapshot rollback operations.

---

## 1️⃣1️⃣ Attempt Remount as Read-Write

```bash
sudo mount -o remount,rw /
```

### Purpose
Attempt to restore write capability without reboot.

### Result
Filesystem remained read-only.

### Conclusion
Kernel-level lock in place.  
Cannot restore write access while mounted.

---

# Phase 6 — Package & Desktop Repair Attempts

---

## 1️⃣2️⃣ Attempt apt update

```bash
sudo apt update
```

### Result

Errors observed:

- Could not create temporary file
- Read-only file system
- Repository updates failed

### Conclusion
Package manager cannot operate due to filesystem lock.

---

## 1️⃣3️⃣ Attempt xRDP/Xorg Reinstall

```bash
sudo apt install -y xorgxrdp xrdp
```

### Result

- Packages already installed
- State write failure due to read-only filesystem

### Conclusion
Desktop failure not caused by missing xRDP packages.

---

# Root Cause Determination

The root filesystem (`/dev/sda2`) is mounted with ext4 flag:

```
emergency_ro
```

### This indicates:

- Filesystem corruption detected
- Kernel automatically switched to read-only mode
- Prevents further damage
- Blocks all write operations

---

# Impact Analysis

As a result:

- Splunk cannot start
- PID files cannot be cleaned
- Desktop sessions cannot initialize properly
- Package management cannot function

---

# Required Remediation

This condition cannot be resolved while the root filesystem is mounted.

### Required action:

- Offline `fsck` on `/dev/sda2`  
**OR**
- Snapshot rollback via ECRL administrative console  

---

# Current Status

## Infrastructure Blocker

### Splunk VM Operational State:

- Network reachable
- SSH functional
- xRDP listening
- Root filesystem locked in emergency read-only mode
- Splunk service down

Administrative recovery required before continuing SOC validation.

---

# End of Week_03 Technical Diagnosis
