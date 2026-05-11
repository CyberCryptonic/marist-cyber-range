# VM Inventory

This file documents the major VM roles used in the Marist Cyber Range.

The exact number of VMs may change as future teams expand the range. This file should be updated whenever a new permanent VM is added.

## Environment Summary

| Environment | Purpose |
|---|---|
| Red Team Environment | Offensive systems and instructor attacker infrastructure |
| Target Environment | Enterprise victim network |
| SOC / Detection Environment | Monitoring, logging, detection, and analysis |

## Target Environment VMs

| VM Role | Purpose |
|---|---|
| Primary Domain Controller | Hosts the main Active Directory domain, DNS, and identity services |
| Backup Domain Controller | Provides redundant domain and DNS services |
| File Server | Hosts department shares and realistic business files |
| Internal Web Server | Hosts internal web content and portal services |
| Windows Log Server | Prepared for centralized Windows event collection |
| Windows 10 User Workstations | Domain-joined user endpoints for realistic activity |
| Windows 11 User Workstations | Domain-joined modern Windows endpoints |
| IT Admin Workstation | Administration system for domain and server management |
| Incident Response Workstation | Defensive investigation system with analysis tools |
| Kali Purple Workstation | Blue team Linux analysis workstation |
| Vulnerable Training Server | Hosts vulnerable applications using Docker |
| Network Traffic Generator | Produces controlled background traffic |

## Red Team Environment VMs

| VM Role | Purpose |
|---|---|
| Student Attacker 01-06 | Kali Linux attacker systems for controlled exercises |
| Instructor Attacker | Instructor-controlled Red Team system |
| Red Team Jump Server | Future controlled access point for Red Team operations |

## SOC / Detection Environment VMs

| VM Role | Purpose |
|---|---|
| Security Onion | SIEM, detection platform, log ingestion, and Fleet management |
| OPNsense Firewall | Segmentation, routing, firewall rules, and syslog forwarding |
| SOC Analyst Workstations | Analyst systems used to access Security Onion and perform investigations |
| Adversary Simulation Server | Hosts MITRE Caldera |
| Range Orchestration Server | Future automation and scenario orchestration |
| Core Network Router | Staged routing system for future expansion |

## Template Strategy

Templates should be maintained for common operating systems.

Recommended templates:

| Template | Purpose |
|---|---|
| Windows Server 2022 Template | Domain controllers, file server, Windows log server |
| Windows 10 Template | User workstations |
| Windows 11 Template | User workstations |
| Ubuntu Server Template | Linux servers, orchestration systems, vulnerable services |
| Ubuntu Desktop Template | Linux desktop systems where needed |
| Kali Linux Template | Red Team attacker systems |
| Kali Purple Template | Blue Team analysis systems |

## VM Documentation Requirements

Each permanent VM should have the following documented:

- VM name
- Hostname
- IP address
- Subnet
- Gateway
- DNS servers
- Operating system
- Domain membership status
- Main role
- Installed tools
- Logging method
- Snapshot status
- Backup status
- Notes for future teams

## Notes

Future teams should keep this file aligned with diagrams, IP allocation, and setup instructions.
