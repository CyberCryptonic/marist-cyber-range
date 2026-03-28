# Stakeholder Questions (Sorted)

## A) Questions for ECRL (Capabilities / Constraints)

**Access + Operations**
- What is the access model (VPN/jump host/accounts/MFA)?
- How is access scheduled (time windows, approvals, on-site only)?
- Can multiple students access simultaneously?

**Compute + Storage**
- Total resource limits available to our project (CPU/RAM/storage)?
- Any per-VM maximums (RAM cap, vCPU cap, disk cap)?
- Storage type and performance expectations?

**Networking**
- Can we create VLANs / segments? If yes, how many?
- Can we control routing between VLANs (L3 rules)?
- Are firewall rules supported? What platform?
- Is Internet egress allowed? If yes, is it filtered or NATed?
- Can we simulate an “external attacker network” inside ECRL?

**Tooling + Restrictions**
- Are there restrictions on what security tools we can install?
- Allowed to run SIEM/IDS/EDR tooling?
- Any banned OS images or tooling lists we must follow?

**Snapshots + Reset**
- Can we snapshot systems?
- Can the environment be reset to a baseline quickly?
- Any retention limits for snapshots?

**Logging / Data**
- Can we export logs off-platform?
- Data retention limits?
- Any monitoring already provided?

---

## B) Questions for Central Hudson (Goals / Scenarios / Success)

**Purpose**
- What is the primary use case (SOC training, red/blue, detection engineering, tabletop, etc.)?
- Who are the intended users (roles, skill level)?

**Scenarios**
- What are the top 5 scenarios you want represented?
- Any high-priority attacker techniques you want simulated?

**Success Criteria**
- What should we demonstrate by April 9 (NTIR checkpoint)?
- What should be fully delivered by May 8?

**Compliance / Constraints**
- Any compliance alignment required (ex: NERC CIP) or internal policy constraints?
- Any tools or approaches you prefer or do NOT want used?

**Deliverables**
- What format do you want the final deliverables in (exec summary, technical report, both)?
- Do you want a repeatable runbook for future student teams?

---

## C) Questions for Professor Foti / Cas (Academic Scope + Deliverables)
- What are the minimum required deliverables for grading?
- What is the priority: technical deployment success vs documentation completeness?
- How should we define “successful cyber range” for this class?
- How should we scope down if ECRL access is delayed?
- NTIR: what counts as acceptable progress for April 9?
