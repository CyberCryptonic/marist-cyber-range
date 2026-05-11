# Source Catalog

This file lists the major documentation sources, official tool references, and project resources used to support the Marist Cyber Range.

The goal is to make it easy for future teams to find the documentation behind the tools and design decisions used in the cyber range.

## Project Repository

| Resource | Purpose | Link |
|---|---|---|
| Marist Cyber Range GitHub Repository | Main source of truth for project documentation, setup guides, scenarios, diagrams, and operational notes | https://github.com/CyberCryptonic/marist-cyber-range |
| Range Setup Instructions | Step-by-step documentation for rebuilding the Target, Red Team, and SOC environments | https://github.com/CyberCryptonic/marist-cyber-range/tree/main/RANGE%20SETUP%20INSTRUCTIONS |

## Virtualization

| Resource | Purpose | Link |
|---|---|---|
| Proxmox VE Downloads | Official download page for Proxmox Virtual Environment | https://www.proxmox.com/en/downloads/proxmox-virtual-environment |
| Proxmox VE Documentation | Official Proxmox documentation for VM management, networking, storage, backups, and administration | https://pve.proxmox.com/pve-docs/ |

## Firewall and Network Segmentation

| Resource | Purpose | Link |
|---|---|---|
| OPNsense Download | Official download page for OPNsense firewall | https://opnsense.org/download/ |
| OPNsense Documentation | Official documentation for firewall rules, interfaces, aliases, routing, and logging | https://docs.opnsense.org/index.html |

## SOC and Detection

| Resource | Purpose | Link |
|---|---|---|
| Security Onion Documentation | Official Security Onion documentation | https://docs.securityonion.net/ |
| Security Onion 2.4 Installation Documentation | Installation reference for the Security Onion 2.4 build used in the project | https://docs.securityonion.net/en/2.4/installation.html |
| Security Onion Current Installation Documentation | Current Security Onion installation documentation for future teams | https://docs.securityonion.net/en/3/main/installation/ |
| Elastic Agent Documentation | Elastic Agent reference material for endpoint telemetry and Fleet-managed agents | https://www.elastic.co/guide/en/fleet/current/fleet-overview.html |

## Adversary Simulation

| Resource | Purpose | Link |
|---|---|---|
| MITRE Caldera Official Site | Official page for MITRE Caldera adversary emulation platform | https://caldera.mitre.org/ |
| MITRE Caldera GitHub Repository | Source repository for MITRE Caldera | https://github.com/mitre/caldera |
| MITRE Caldera Installation Documentation | Installation reference for building and running Caldera | https://caldera.readthedocs.io/en/latest/Installing-Caldera.html |
| MITRE ATT&CK | Framework used to describe adversary tactics, techniques, and procedures | https://attack.mitre.org/ |

## Red Team and Linux Tooling

| Resource | Purpose | Link |
|---|---|---|
| Kali Linux Documentation | Documentation for Kali Linux attacker systems | https://www.kali.org/docs/ |
| Kali Purple | Kali Linux defensive/security operations distribution reference | https://www.kali.org/get-kali/#kali-platforms |
| tcpdump Manual | Packet capture and traffic validation reference | https://www.tcpdump.org/manpages/tcpdump.1.html |
| Wireshark Documentation | Packet analysis documentation | https://www.wireshark.org/docs/ |

## Vulnerable Training Applications

| Resource | Purpose | Link |
|---|---|---|
| OWASP Juice Shop | Intentionally vulnerable web application used for training | https://owasp.org/www-project-juice-shop/ |
| OWASP Juice Shop GitHub | Source repository for Juice Shop | https://github.com/juice-shop/juice-shop |
| DVWA GitHub | Damn Vulnerable Web Application source repository | https://github.com/digininja/DVWA |

## Windows Enterprise Infrastructure

| Resource | Purpose | Link |
|---|---|---|
| Microsoft Active Directory Domain Services | Reference for AD DS concepts and deployment | https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview |
| Group Policy Documentation | Reference for Windows Group Policy management | https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-overview |
| Windows Event Forwarding | Reference for centralized Windows event collection | https://learn.microsoft.com/en-us/windows/security/operating-system-security/device-management/use-windows-event-forwarding-to-assist-in-intrusion-detection |

## Linux Logging

| Resource | Purpose | Link |
|---|---|---|
| rsyslog Documentation | Reference for Linux log forwarding | https://www.rsyslog.com/doc/ |
| systemd journalctl Documentation | Reference for Linux system log review | https://www.freedesktop.org/software/systemd/man/latest/journalctl.html |

## Notes

Future teams should add sources here whenever they introduce new tools, detection logic, scenarios, or major design changes.
