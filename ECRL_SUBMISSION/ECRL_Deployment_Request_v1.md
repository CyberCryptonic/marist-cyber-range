# ECRL Deployment Request v1 — Marist Cyber Range

## 1) Project Summary
This project is a controlled cyber range hosted within ECRL to support utility-sector cybersecurity training and simulation aligned to Central Hudson priorities. The environment will support segmented networking, logging/monitoring visibility, and repeatable exercise execution with baseline reset capability where possible.

## 2) Requested Environment Overview
- Hosting Platform: ECRL-managed environment
- Internet Access: **TBD (requested if permitted for updates/feeds)**
- Segmentation: Multiple network segments (see Network Requirements)
- Baseline Reset: Snapshot/restore or rebuild guidance requested

## 3) VM Inventory (Initial Request — v1)
> NOTE: Specific counts/resources can be adjusted based on ECRL limits.

| VM Name | Role / Purpose | OS | vCPU | RAM | Storage |
|---|---|---|---:|---:|---:|
| SIEM-01 | Central log collection + analysis | TBD | TBD | TBD | TBD |
| DC-01 | Active Directory / identity services (optional) | TBD | TBD | TBD | TBD |
| WS-01 | User workstation (victim/employee) | TBD | TBD | TBD | TBD |
| WS-02 | User workstation (victim/employee) | TBD | TBD | TBD | TBD |
| LNX-01 | Linux server (app/service target) | TBD | TBD | TBD | TBD |
| ATK-01 | Internal attacker simulation box (controlled) | TBD | TBD | TBD | TBD |

## 4) Network Requirements
Requested segments (logical):
- **Mgmt/Admin Network**: admin access to manage systems
- **User Network**: workstations
- **Server Network**: servers / services
- **Security/Monitoring Network**: SIEM/IDS/monitoring
- **Attack Simulation Network (optional)**: controlled adversary simulation

Routing + Controls:
- Inter-VLAN routing: **TBD based on ECRL capability**
- Firewall rules: allow only required traffic between segments (principle of least privilege)
- Internet egress: **TBD based on ECRL policy**

## 5) Security + Logging Requirements
- Centralized logging to SIEM-01 (or ECRL-supported alternative)
- Collect logs from:
  - Windows event logs (if Windows hosts are used)
  - Syslog from Linux servers
  - Network/security device logs if available
- Retention: **TBD**
- Export: **TBD** (whether logs can be exported off-platform)

## 6) Access Requirements
- Students require access to configure the environment once approved
- Access method: **TBD** (VPN/jump host/on-site)
- Authentication: **TBD** (accounts/MFA)
- Scheduling: request guidance on best process to book lab time

## 7) Assumptions + Constraints
- We will not be building local VMs; all deployment occurs within ECRL
- Final design must conform to ECRL resource and tooling constraints
- We will adjust VM count/specs after ECRL capability confirmation

## 8) Open Questions for ECRL
- What are the total compute/storage/network limits available?
- Are VLANs / segmentation supported? How many?
- Is firewall policy enforcement supported?
- Is Internet access allowed for updates?
- Snapshot/restore/reset options available?
- Any restricted tooling/software list?
- Can logs be exported externally, and what retention limits apply?
- Are there scheduled maintenance times?
