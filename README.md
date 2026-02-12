# Marist Cyber Range (SOC Build & Ops)

## Purpose
This repository is the official documentation and project hub for building a reusable cyber range for Marist University. The goal is a scalable environment (30+ VMs baseline) that supports SOC-style monitoring, scenario-based training, and long-term handoff to future student teams.

## Stakeholders
- Marist University Cybersecurity Program
- Partner: Central Hudson (Poughkeepsie, NY)
- Faculty Advisor: Dominick Foti
- Student Team: Nate Pena, Erick Perez, Ryan Clark, & Benjamin Brandt

## What we are building (Semester Scope)
- Range architecture designed for ~30 VMs with future scaling
- Network segmentation (zones/VLANs) and safe isolation boundaries
- Central telemetry pipeline (endpoint + server + identity + network)
- SIEM + detections (tooling decision pending)
- Scenario library (repeatable execution + expected detections + evidence)
- Operations runbooks (reset/rebuild, access model, class usage)

## Repo Structure (where everything lives)
- `/docs/` — official documentation (requirements, architecture, network, operations)
- `/scenarios/` — scenario playbooks (setup → execution → expected telemetry → evidence → reset)
- `/diagrams/` — architecture/topology/dataflow diagrams
- `/evidence/` — screenshots/logs proving builds and detections
- `/references/` — Zotero/BibTeX export and citation notes

## How we work (Definition of Done)
An item is only “Done” when:
- Documentation is updated in `/docs/` (or scenario file in `/scenarios/`)
- Evidence is attached in `/evidence/` (screenshots/logs/notes)
- A teammate reviews and comments “Reviewed” on the issue

## Quick Links
- Requirements (Working): /docs/02_requirements.md
- Architecture (Draft): /docs/03_architecture-draft.md
- Stakeholder Questions (Week 02): /DOCUMENTATION/Stakeholder_Questions.md
- ECRL Deployment Request v1 (Week 02): /ECRL_SUBMISSION/ECRL_Deployment_Request_v1.md
- Detailed Semester Timeline (Week 02): /DOCUMENTATION/Detailed_Semester_Timeline.md
- Weekly Execution (Week 02): /WEEKLY_EXECUTION/Week_02/
- Meeting Notes: /docs/09_meeting-notes.md

## Project Tracking
Detailed task tracking is maintained in a private GitHub Project board during the semester (internal assignments/notes). High-level milestones and weekly progress are documented in this repository (ROADMAP + WEEKLY_EXECUTION + meeting notes).
