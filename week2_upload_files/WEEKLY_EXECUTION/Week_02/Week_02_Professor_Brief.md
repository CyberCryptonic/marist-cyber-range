# Week 02 — Professor Brief (Meeting Ready)

**Project:** Marist Cyber Range (ECRL-hosted)  
**Week:** 02 (Execution)  
**Date Prepared:** Feb 11, 2026  
**Prepared By:** Project Team  

---

## 1) Where We Are Right Now
- Week 1 foundational documentation is complete in GitHub
- The cyber range will be deployed through **ECRL** (we will not be building local VMs locally)
- Our next step is converting project requirements into an **ECRL deployment request** and separating questions by stakeholder so meetings are efficient and productive

---

## 2) What Changed Since Week 1 (This Week’s Progress)
- Stakeholder question separation plan:
  - **ECRL** = environment capabilities/limits + access model
  - **Central Hudson** = goals, scenarios, success criteria
  - **Faculty** = academic scope + deliverables expectations
- Formal **ECRL Deployment Request v1** started
- Detailed semester timeline through May 8 started

---

## 3) Decisions / Guidance Needed Today
1. Confirm our stakeholder routing (ECRL vs Central Hudson) is correct
2. Confirm what "success" must look like by:
   - **April 9 (NTIR checkpoint)**
   - **May 8 (final delivery)**
3. Confirm minimum technical scope vs documentation scope expectations (what to prioritize if access is delayed)

---

## 4) What We Need From ECRL (Capabilities + Limits)
Top items we need answered:
- Access model (accounts, MFA, VPN/jump host, scheduling)
- Resource limits (CPU/RAM/storage totals + per-VM limits)
- Networking capabilities (VLANs, routing, firewall, NAT, Internet egress)
- Tooling/install limitations (what software is allowed)
- Snapshot/restore policy (reset between exercises, rollback support)
- Log export options and data retention limits

---

## 5) What We Need From Central Hudson (Client Goals)
Top items we will ask:
- Primary purpose of the range (SOC training, red/blue, tabletop, detection engineering, etc.)
- Top threat scenarios they care most about
- Success criteria they want to see by April vs May
- Any compliance alignment (ex: NERC CIP) or internal policy constraints
- Intended users + skill levels
- Preferred deliverables format (exec summary, technical report, both)

---

## 6) Week 02 Deliverables (GitHub)
By end of Week 2 we will have:
- Stakeholder Questions document finalized
- ECRL Deployment Request v1 drafted (with TBDs where needed)
- Detailed semester timeline through May 8
- Week 02 action plan + checklist
- Central Hudson meeting agenda for Thursday

---

## 7) Risks / Blockers (Early)
- ECRL access/approval timing could delay configuration
- Tooling restrictions could impact monitoring stack choices
- Client scope ambiguity could lead to rework if not clarified early
