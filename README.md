# Marist Cyber Range (SOC Build & Ops)

## Overview
This repository documents the design, development, and implementation of a virtual cyber range for Marist University. The environment is built to simulate real-world enterprise networks and support hands-on cybersecurity training across Red Team, Blue Team, and SOC roles.

The goal is to create a reusable and scalable platform that future student teams can continue to expand and improve.

---

## Stakeholders
- Marist University Cybersecurity Program  
- Industry Partner: Central Hudson Gas & Electric  
- Faculty Advisor: Dominick Foti  
- Student Team: Nate Pena, Erick Perez, Ryan Clark, Benjamin Brandt  

---

## What We Are Building
- Virtualized cyber range hosted on a Proxmox hypervisor  
- ~30 virtual machines across three environments:
  - Red Team (attack simulation)
  - Target / Blue Team (defensive systems)
  - SOC / Detection (monitoring and analysis)
- Network segmentation using isolated subnets:
  - Red Team: 10.20.10.0/24  
  - Target: 10.20.20.0/24  
  - SOC: 10.20.30.0/24  
- Centralized monitoring stack (Security Onion – includes Zeek, Suricata, ELK)
- Scenario-based training environment for realistic attack/defense exercises  
- Operational documentation for setup, reset, and long-term use  

---

## Architecture Summary
The cyber range is deployed on a single Proxmox server hosted in the ECRL.  
Each environment is logically segmented and connected through a firewall/router to simulate enterprise network behavior while maintaining isolation.

The system is designed to:
- Support realistic attack and detection workflows  
- Generate meaningful logs and alerts  
- Allow controlled interaction between environments  

---

## Repository Structure
- `/docs/` — Architecture, requirements, network design, and operations  
- `/scenarios/` — Attack scenarios and execution workflows  
- `/diagrams/` — Topology and architecture visuals  
- `/evidence/` — Screenshots and logs validating system functionality  
- `/references/` — Research materials and citations  

---

## How We Work (Definition of Done)
An issue is considered complete when:
- Relevant documentation is updated (`/docs/` or `/scenarios/`)  
- Supporting evidence is added (`/evidence/`)  
- A teammate reviews and confirms completion  

---

## Project Progression
The project follows a structured, real-world workflow:

1. Planning & Design (Weeks 1–7)  
2. Infrastructure & Networking (Week 8)  
3. Environment Access & Tooling (Week 9)  
4. Scenario Development (Week 10)  
5. Deployment Preparation (Week 11)  
6. System Integration & Testing (Week 12)  
7. Finalization & Presentation (Week 13)  

---

## Weekly Documentation
All weekly progress, goals, and work logs are tracked in:
`/WEEKLY_EXECUTION/`


Each week contains:
- Goals  
- Timeline  
- Work Log  

---

## Project Tracking
Task tracking and workflow management are handled through GitHub Projects.  
This repository serves as the source of truth for all technical documentation, system design, and implementation artifacts.

---

## Purpose of This Repository
This repository is intended to:
- Document the full build of the cyber range  
- Provide a reference for future student teams  
- Support presentations and stakeholder communication  
- Demonstrate a structured approach to building a SOC environment  

---
