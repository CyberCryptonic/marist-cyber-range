# Phase_02 — SOC Environment Setup

## Status

✅ COMPLETE

# Marist SOC Cyber Range
# Lab Build Guide — Phase 02: Firewall Segmentation Server and Core Network Router Deployment

---

# Phase Overview

Phase 02 focused on building the routing and segmentation layer inside the SOC / Detection Environment.

This phase documents the systems that were completed and validated during this stage of the build:

- Firewall-Segmentation-Server (OPNsense)
- Core-Network-Router

The purpose of this phase was to place a dedicated firewall between the Target Environment and the SOC / Detection Environment, enforce segmentation rules, restrict administrative access to the firewall to SOC systems only, and begin forwarding firewall telemetry into Security Onion. This phase also documents the successful baseline setup of the Core-Network-Router, which was prepared for future scenarios but intentionally left out of the active routing path for the current project.

> Important scope note: This guide documents only the final successful build path and only the steps that were completed successfully. Failed attempts, unfinished logging work, and later cross-environment integrations are intentionally excluded from this phase.

---

# Phase 02 Objectives

- Deploy a dedicated firewall / segmentation VM using OPNsense  
- Connect OPNsense to both the SOC network and the Target network  
- Assign static interface IPs for both network segments  
- Use OPNsense as the active segmentation device  
- Restrict firewall GUI access to SOC systems only  
- Block Target Environment access to firewall management  
- Forward firewall logs to Security Onion  
- Validate firewall logs inside Security Onion  
- Build and prepare the Core-Network-Router for future use  

---

# Final Outcome

- OPNsense deployed and operational  
- WAN (SOC side): 10.20.30.20/24  
- LAN (Target side): 10.20.20.1/24  
- Firewall GUI restricted to SOC network  
- Target network blocked from firewall GUI  
- OPNsense logs successfully sent to Security Onion  
- Logs visible in Security Onion Hunt  
- Core-Network-Router built and stabilized  
- Core router reserved for future use only  

---

# Important Design Notes

## OPNsense as Active Segmentation Device

OPNsense is the ONLY active routing and segmentation device in this phase.

The Core-Network-Router is NOT used for routing in this phase.

---

## Firewall Management Restriction

- SOC network → allowed to access firewall GUI  
- Target network → blocked from firewall GUI  

---

## Logging Architecture

- OPNsense → Security Onion via syslog  
- Logs validated in Security Onion Hunt  

---

## Core Router Role

- Built and configured  
- Not used in routing path  
- Reserved for future expansion  

---

# 1. Build Firewall-Segmentation-Server VM

## 1.1 Upload OPNsense ISO

Upload to Proxmox:

OPNsense-25.1-dvd-amd64.iso

---

## 1.2 Create VM

Name: Firewall-Segmentation  

Attach ISO during creation  

---

## 1.3 Hardware Configuration

Memory: ~8 GB  
CPU: 4 cores  
Machine: q35  
Disk: ~65 GB  
SCSI: VirtIO  

---

## 1.4 Network Configuration

net0 → vmbr3 (SOC network)  
net1 → vmbr2 (Target network)  

Disable Proxmox firewall on both NICs  

---

# 2. Install OPNsense

- Boot from ISO  
- Complete installation  
- Reboot into console  

---

# 3. Assign Interfaces

From console:

Assign interfaces:

WAN → vtnet0 (SOC)  
LAN → vtnet1 (Target)  

---

# 4. Configure Interface IPs

## 4.1 LAN (Target)

IP: 10.20.20.1  
Subnet: /24  
Gateway: none  

---

## 4.2 WAN (SOC)

IP: 10.20.30.20  
Subnet: /24  

---

## 4.3 Final Layout

WAN → 10.20.30.20  
LAN → 10.20.20.1  

---

# 5. Access Web GUI

From SOC workstation:

https://10.20.30.20  

Login with admin credentials  

---

# 6. Configure Firewall Rules

## 6.1 Allow SOC → Firewall GUI

Firewall → Rules → WAN  

Allow:

Source: 10.20.30.0/24  
Destination: WAN address  
Port: 443  

---

## 6.2 Block Non-SOC GUI Access

Block:

Source: any  
Destination: WAN address  
Port: 443  

---

## 6.3 Block Target → Firewall GUI

Firewall → Rules → LAN  

Block:

Source: 10.20.20.0/24  
Destination: WAN address  
Port: 443  

Enable logging on this rule  

---

# 7. Configure Logging to Security Onion

## 7.1 OPNsense Logging

System → Settings → Logging → Remote  

Enable:

Transport: UDP  
IP: 10.20.30.10  
Port: 514  

---

## 7.2 Security Onion Configuration

Administration → Configuration → syslog  

Add:

10.20.30.20  

Synchronize firewall  

---

# 8. Validate Logging

## 8.1 Generate Traffic

From Target machine:

Attempt access to:

https://10.20.30.20  

---

## 8.2 Verify in OPNsense

Firewall → Live Logs  

Confirm blocked entries  

---

## 8.3 Verify in Security Onion

Hunt → filterlog  

Confirm logs appear  

---

# 9. Build Core-Network-Router

## 9.1 Create VM

Name: Core-Network-Router  

Install Ubuntu Server  

---

## 9.2 Assign Network

Primary NIC → SOC network  

---

## 9.3 Configure Static IP

IP: 10.20.30.1  
Subnet: /24  

---

## 9.4 Add Second NIC

Attach second NIC for future routing  

Do NOT use it in this phase  

---

## 9.5 Clean Routing

Ensure no conflicting routes  

OPNsense remains active router  

---

## 9.6 Final State

- Router reachable  
- Not handling traffic  
- Reserved for future scenarios  

---

# 10. Validation Checklist

## OPNsense

- Reachable from SOC  
- GUI accessible  
- Target blocked from GUI  
- Logs sent to Security Onion  

## Security Onion

- Logs visible in Hunt  
- filterlog entries present  

## Core Router

- Reachable  
- Static IP set  
- Not interfering with routing  

---

# Phase 02 Complete

Environment now includes:

- Firewall segmentation via OPNsense  
- SOC-only firewall management access  
- Firewall logs integrated into SIEM  
- Core router staged for future use  

---

# Next Phase

- Complete remaining SOC systems  
- Configure Windows log pipeline  
- Configure Linux log pipeline  
- Final integration between Target and SOC environments  

---

End of Phase 02
