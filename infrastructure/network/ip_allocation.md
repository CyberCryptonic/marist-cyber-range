# IP Allocation Plan

This file documents the major IP addressing plan for the Marist Cyber Range.

The cyber range is separated into three primary environments:

- Red Team Environment
- Target Environment
- SOC / Detection Environment

## Network Summary

| Environment | Subnet | Purpose |
|---|---|---|
| Red Team Environment | `10.20.10.0/24` | Attacker systems and offensive training infrastructure |
| Target Environment | `10.20.20.0/24` | Enterprise victim network |
| SOC / Detection Environment | `10.20.30.0/24` | Monitoring, detection, and analyst infrastructure |

## Target Environment

| System | Example IP | Purpose |
|---|---:|---|
| Primary Domain Controller | `10.20.20.10` | Active Directory, DNS, identity services |
| Backup Domain Controller | `10.20.20.11` | Redundant AD DS and DNS services |
| File Server | `10.20.20.12` | Department file shares and role-based access |
| Internal Web Server | `10.20.20.13` | Internal web portal |
| Vulnerable Training Server | `10.20.20.14` | DVWA, Juice Shop, vulnerable services |
| Network Traffic Generator | `10.20.20.15` | Background traffic generation and testing |
| Windows Log Server | `10.20.20.16` | Windows log collection preparation |
| Windows Workstations | `10.20.20.x` | Domain-joined user endpoints |
| Linux Workstations / Servers | `10.20.20.x` | Linux endpoints and validation systems |
| Target Gateway | `10.20.20.1` | OPNsense LAN-side gateway for Target subnet |

## SOC / Detection Environment

| System | Example IP | Purpose |
|---|---:|---|
| Security Onion | `10.20.30.10` | SIEM, log ingestion, detection, Fleet management |
| OPNsense SOC Interface | `10.20.30.20` | Firewall SOC-side interface |
| SOC Analyst Workstations | `10.20.30.x` | Analyst access to Security Onion and SOC tools |
| Adversary Simulation Server | `10.20.30.x` | MITRE Caldera |
| Range Orchestration Server | `10.20.30.x` | Future automation, scripts, and orchestration |
| SOC Gateway | `10.20.30.1` | Gateway for SOC subnet |

## Red Team Environment

| System | Example IP | Purpose |
|---|---:|---|
| Student Attacker 01 | `10.20.10.x` | Kali Linux attacker system |
| Student Attacker 02 | `10.20.10.x` | Kali Linux attacker system |
| Student Attacker 03 | `10.20.10.x` | Kali Linux attacker system |
| Student Attacker 04 | `10.20.10.x` | Kali Linux attacker system |
| Student Attacker 05 | `10.20.10.x` | Kali Linux attacker system |
| Student Attacker 06 | `10.20.10.x` | Kali Linux attacker system |
| Instructor Attacker | `10.20.10.x` | Instructor-controlled attacker system |
| Red Team Jump Server | `10.20.10.x` | Controlled Red Team access point |

## Addressing Rules

Future teams should follow these rules:

1. Keep infrastructure servers on static IP addresses.
2. Keep domain controllers, Security Onion, firewall interfaces, and core servers documented.
3. Do not reuse IP addresses.
4. Update this file immediately when a new permanent system is added.
5. Avoid placing student workstations or temporary test systems in reserved infrastructure ranges.
6. Keep DHCP ranges separate from static infrastructure systems if DHCP is later introduced.

## Reserved Addressing Concept

Recommended reserved ranges:

| Range | Suggested Use |
|---|---|
| `.1 - .20` | Core infrastructure |
| `.21 - .49` | Servers |
| `.50 - .99` | Administrative and SOC systems |
| `.100 - .199` | Workstations and student systems |
| `.200 - .249` | Temporary testing |
| `.250 - .254` | Reserved |

## Maintenance

Any change to IP addressing should also be reflected in:

- Diagrams
- Scenario documentation
- Firewall notes
- Security Onion allowlists
- Elastic Agent enrollment notes
- Troubleshooting guides
