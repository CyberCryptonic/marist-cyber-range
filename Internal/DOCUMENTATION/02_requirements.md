> **Status:** Draft   
> **Last Updated:** 2/5/26  
> **Purpose:** Define functional and non-functional requirements for the Marist cyber range and SOC training environment.

# 02 – Requirements

Status: Draft  
Last Updated: 2/5/26  
Purpose: Define functional and non-functional requirements for the Marist Cyber Range and SOC training environment.

---

## 1. Project Objective

Design and deploy a scalable, scenario-driven cyber range within ECRL that supports:

- Student-driven cybersecurity research
- Faculty-adoptable structured curriculum labs
- Real-world SOC training workflows
- Repeatable scenario execution and reset capability
- Long-term sustainability beyond a single semester

---

## 2. Functional Requirements

### 2.1 Access & User Model
- Students must access the environment via Marist VPN.
- Multiple students must be able to access simultaneously.
- Faculty must have oversight access to validate student work.
- Admin-level access limited to designated project maintainers.

### 2.2 Scenario Execution
- The range must support structured cyber attack scenarios.
- Each scenario must include:
  - Defined objectives
  - Attack steps
  - Expected telemetry/log generation
  - Detection logic
  - Validation criteria
  - Reset instructions
- Scenarios must be reproducible and documented.

### 2.3 SOC Telemetry
The environment must generate:
- Endpoint logs (Windows + Linux)
- Network logs
- Identity/authentication logs
- Application logs (web/database where applicable)

All telemetry must flow to the central monitoring platform (e.g., Splunk or approved SIEM).

### 2.4 Detection & Response
The SOC layer must support:
- Search queries
- Correlation rules
- Alert generation
- Dashboard visualization
- Investigation workflows
- Evidence collection

Students must be able to:
- Receive alerts
- Investigate events
- Correlate logs
- Document findings
- Recommend containment actions

### 2.5 Reset & Recovery
- A clean baseline must exist.
- Snapshots used sparingly.
- Reinstall process documented.
- Scenario resets must be achievable without full rebuild.
- Backups are the responsibility of the project team.

---

## 3. Non-Functional Requirements

### 3.1 Safety & Isolation
- Internal-only attack simulation.
- No uncontrolled outbound attack traffic.
- No modification of core Marist network.
- VLANs provisioned only by ECRL.

### 3.2 Scalability
- Architecture must support expansion to 30+ VMs.
- Must support concurrent student usage.
- Scenario pods must be modular.

### 3.3 Maintainability
- All configurations documented in GitHub.
- Reproducible VM builds.
- Clear folder structure.
- No reliance on undocumented manual steps.

### 3.4 Availability Reality
- 24/7 access expected.
- No guaranteed live support.
- Team must operate independently.
- Environment must tolerate rebuild events.

---

## 4. ECRL Constraints

- Access via VPN only.
- VLANs provisioned by ECRL.
- Routing not managed by project team.
- Firewall rule changes require Marist IT coordination.
- Outbound internet allowed under institutional controls.
- Limited GPU availability.
- Snapshots allowed but limited.
- Team responsible for backups and operational management.

---

## 5. Acceptance Criteria

The cyber range is considered operational when:

- At least 5 structured scenarios are implemented.
- Each scenario has documented learning objectives.
- Telemetry flows correctly into the SIEM.
- Detection rules successfully trigger for each scenario.
- Faculty can validate student work in under 5 minutes.
- Reset process is documented and tested.
- Architecture documentation is complete and reproducible.
