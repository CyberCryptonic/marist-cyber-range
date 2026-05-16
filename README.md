# Marist Cyber Range (SOC Build & Ops)

## Overview

This repository documents the design, development, and implementation of the Marist Cyber Range, a virtual cybersecurity training environment built to simulate realistic enterprise security operations.

The range supports hands-on learning across Red Team, Blue Team, and SOC roles by combining enterprise infrastructure, segmented networking, vulnerable services, centralized monitoring, adversary simulation, and scenario-based training.

The goal of this project is to create a reusable, scalable, and well-documented cyber range that future student teams can continue to expand, improve, and use for cybersecurity education.

---

## Responsible Use

This project is intended for controlled cybersecurity education, research, and defensive security training.

Offensive tooling, adversary simulation, scanning, vulnerable applications, and traffic generation should only be used inside an isolated lab environment or another environment where explicit authorization has been granted.

Do not use this material to target systems, networks, users, or organizations without permission.

---

## Stakeholders

- Marist University Cybersecurity Program
- Industry Partner: Central Hudson Gas & Electric
- Faculty Advisor: Dominick Foti
- Student Team: Nate Pena, Erick Perez, Ryan Clark, Benjamin Brandt

---

## What We Built

The Marist Cyber Range includes:

- A virtualized cyber range hosted on Proxmox
- Approximately 30 virtual machines across multiple segmented environments
- A Red Team environment for controlled attacker activity
- A Target environment that simulates an enterprise network
- A SOC / Detection environment for monitoring, alerting, and investigation
- Active Directory, DNS, domain users, groups, and Group Policy
- Department-based file shares with role-based access control
- Internal web services
- Vulnerable training applications
- Security Onion for centralized monitoring and detection
- OPNsense for firewall segmentation and routing
- Elastic Agent endpoint telemetry
- Linux syslog forwarding
- MITRE Caldera for adversary simulation
- Network traffic generation for background activity
- Backup and snapshot procedures for safe rollback
- Scenario playbooks for future student training

---

## Network Segmentation

The cyber range is logically segmented into three primary environments:

| Environment | Subnet | Purpose |
|---|---|---|
| Red Team Environment | `10.20.10.0/24` | Offensive systems and controlled attacker activity |
| Target Environment | `10.20.20.0/24` | Enterprise victim network with users, servers, services, and vulnerable applications |
| SOC / Detection Environment | `10.20.30.0/24` | Security Onion, analyst systems, firewall management, logging, and detection tooling |

The environment is designed to simulate enterprise network behavior while maintaining isolation and controlled interaction between systems.

---

## Architecture Summary

The cyber range is deployed on a Proxmox virtualization host. Each environment is separated by subnet and connected through controlled firewall and routing paths.

The system is designed to:

- Support realistic attack-to-detection workflows
- Generate meaningful logs, alerts, and network telemetry
- Allow students to practice SOC investigation and documentation
- Provide safe rollback using snapshots and backups
- Support future automation and scenario development

---

## Core Tools and Platforms

| Tool / Platform | Purpose |
|---|---|
| Proxmox VE | Virtualization platform |
| OPNsense | Firewall, routing, and segmentation |
| Security Onion | SIEM, monitoring, detection, and telemetry review |
| Elastic Agent | Endpoint telemetry collection |
| MITRE Caldera | Adversary simulation |
| Kali Linux | Red Team attacker systems |
| Kali Purple | Blue Team analysis workstation |
| Windows Server | Active Directory, DNS, file services, and logging infrastructure |
| Ubuntu Server | Linux servers, vulnerable services, orchestration, and support systems |
| Docker | Hosting vulnerable applications |
| DVWA | Vulnerable web application training target |
| OWASP Juice Shop | Vulnerable web application training target |
| rsyslog | Linux log forwarding |
| hping3 / iperf3 | Traffic generation and validation |

---

## Repository Structure

| Folder / File | Purpose |
|---|---|
| `RANGE SETUP INSTRUCTIONS/` | Step-by-step documentation for rebuilding the cyber range |
| `infrastructure/` | Automation, network design, provisioning notes, baselines, and configuration references |
| `scenarios/` | Scenario playbooks using setup, execution, expected telemetry, detection, evidence, and reset format |
| `diagrams/` | Network topology and architecture visuals |
| `references/` | Source catalog, Zotero workflow, and citation exports |
| `WEEKLY_EXECUTION/` | Weekly goals, progress logs, and project timeline notes |
| `SECURITY.md` | Responsible reporting and security policy |
| `CONTRIBUTING.md` | Contribution guidelines |
| `LICENSE` | Project license |

---

## Quick Links

- [Range Setup Instructions](./RANGE%20SETUP%20INSTRUCTIONS)
- [Infrastructure Documentation](./infrastructure)
- [Scenario Playbooks](./scenarios)
- [References](./references)
- [Security Policy](./SECURITY.md)
- [Contributing Guide](./CONTRIBUTING.md)
- [License](./LICENSE)

---

## Project Progression

The project followed a structured workflow:

1. Planning and design
2. Proxmox infrastructure setup
3. Network segmentation
4. Target Environment build
5. Active Directory and enterprise services
6. Red Team Environment build
7. SOC / Detection Environment build
8. Security Onion integration
9. OPNsense firewall and telemetry forwarding
10. Elastic Agent and Linux syslog forwarding
11. MITRE Caldera and orchestration preparation
12. Traffic generation and validation
13. Backup and snapshot documentation
14. Scenario framework development
15. Final documentation and presentation

---

## Definition of Done

A task or issue is considered complete when:

- The relevant documentation is updated
- Supporting evidence or screenshots are added when useful
- The change is reviewed for accuracy
- Sensitive information is removed or sanitized
- The change supports authorized lab use only
- The environment can be rebuilt or validated from the documentation

---

## Purpose of This Repository

This repository is intended to:

- Document the full build of the Marist Cyber Range
- Provide a reference for future student teams
- Support cybersecurity education and hands-on training
- Demonstrate a structured approach to building a SOC environment
- Help others recreate a similar range using their own authorized hardware and lab environment
- Preserve lessons learned from the semester-long project

---

## License

This project is licensed under the MIT License.

The documentation, setup instructions, scripts, and configuration examples are provided so students, educators, and cybersecurity teams can study, adapt, and recreate the Marist Cyber Range in their own authorized lab environments.

See the [LICENSE](LICENSE) file for details.
