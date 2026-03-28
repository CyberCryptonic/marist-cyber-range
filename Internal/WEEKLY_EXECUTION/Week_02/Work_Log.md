# Week_02 — Work Log

## Overview
Week 02 focused on stakeholder alignment, infrastructure clarification with ECRL, formal deployment documentation drafting, and locking the semester execution roadmap.  
This week transitions the project from conceptual planning into structured operational preparation.

---

# Tasks

- [x] Finalize `Stakeholder_Questions.md` (sorted by stakeholder)
- [x] Draft `ECRL_Deployment_Request_v1.md` (no blanks, TBD allowed)
- [x] Publish `Detailed_Semester_Timeline.md` through May 8
- [x] Create Central Hudson Thursday agenda (client questions only)
- [x] Draft NTIR abstract (deadline Feb 15)

---

## Task Details

### Finalize `Stakeholder_Questions.md`

- Organized by stakeholder:
  - ECRL / Marist IT
  - Central Hudson
  - Faculty
  - Students (end users)
- Grouped questions by:
  - Infrastructure
  - Access model
  - Security controls
  - Scalability
  - Validation expectations
- Prepared for structured stakeholder meetings

---

### Draft `ECRL_Deployment_Request_v1.md`

- No blank sections (used `TBD` where required)
- Included:
  - Architecture overview
  - VLAN provisioning requirements
  - VPN-based access model
  - Outbound internet clarification
  - Snapshot usage policy
  - Telemetry and SIEM requirements
  - Estimated VM scaling plan
- Structured for formal review and approval

---

### Publish `Detailed_Semester_Timeline.md`

Phased plan through May 8:

1. Infrastructure stabilization
2. Core environment deployment
3. Build initial 3–5 scenarios
4. Detection engineering + dashboards
5. Faculty validation package
6. Documentation freeze + presentation preparation

Milestones and dependencies included.

---

### Create Central Hudson Agenda (Client Questions Only)

Agenda focused on:

- Business use-case alignment
- Desired learning outcomes
- Industry realism expectations
- Detection engineering requirements
- Definition of “success”
- Long-term adoption vision

No internal technical deep dive — stakeholder-facing only.

---

### Draft NTIR Conference Abstract

Abstract highlights:

- Student-driven research cyber range
- Faculty-adoptable curriculum framework
- Real-world SOC workflow replication
- Controlled VLAN-segmented architecture within ECRL
- Long-term sustainability beyond a single semester

---

# Meeting Notes (Professor)

## Summary
- Confirmed direction: student-driven cyber range usable by faculty.
- Emphasis on sustainability and documentation quality.
- Reinforced structured scenario library approach.
- Validated two-lane model (Curriculum Mode + Research Mode).

---

## Action Items

- Submit formal ECRL deployment request.
- Finalize NTIR abstract before Feb 15.
- Refine Central Hudson scenario goals.
- Continue architecture documentation refinement.
- Begin defining first 3 foundational scenarios.

---

## Decisions Locked

- Access via VPN.
- Environment available 24/7 (no live support).
- Multiple students may access simultaneously.
- VLANs provisioned by ECRL (no self-managed routing).
- Outbound internet allowed (institutionally controlled).
- Team responsible for backups and operational management.
- Snapshots allowed but must be used sparingly.
- Tooling broadly allowed (avoid paid licenses).

---

# Risks / Blockers

- Waiting on ECRL capability limits and access process.
- Waiting on Central Hudson goals and success criteria.
- Potential delay if ECRL approval is slower than expected.
- Hypervisor platform and storage limits not yet confirmed.
- Traffic mirroring capability (SPAN/TAP) unconfirmed.

---

# Artifacts Produced

- `/DOCUMENTATION/Stakeholder_Questions.md`
- `/ECRL_SUBMISSION/ECRL_Deployment_Request_v1.md`
- `/DOCUMENTATION/Detailed_Semester_Timeline.md`
- `/WEEKLY_EXECUTION/Week_02/*`
- Architecture diagrams
- Network zone documentation
- Telemetry flow documentation
- Scenario pod framework

---

# Week 02 Status

**Status:** Complete  
**Phase Transition:** Planning → Structured Deployment Preparation  
**Next Phase:** Infrastructure provisioning + Scenario implementation
