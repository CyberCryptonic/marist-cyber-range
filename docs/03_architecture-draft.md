> **Status:** Draft    
> **Last Updated:** 2/5/26
> **Purpose:** Document the initial architecture for a scalable 30+ VM cyber range with SOC telemetry and scenario support.

# 03 – Architecture Draft

Status: Draft  
Last Updated: 2/5/26  
Purpose: Document the initial architecture for a scalable 30+ VM cyber range with SOC telemetry and scenario support.

---

## 1. Architectural Philosophy

The Marist Cyber Range operates under a two-lane model:

1. Curriculum Mode (Faculty-Adoptable)
2. Research Mode (Student-Driven Expansion)

Both modes share a stable foundational infrastructure while allowing scenario-based modular expansion.

---

## 2. High-Level Architecture

### Core Components

- SOC / SIEM Server
- Domain Controller (Active Directory)
- Windows Workstations (2–5 minimum)
- Linux Server
- Web/Application Server
- Database Server
- Attacker VM (Internal Red Team)
- Network Sensor (optional: Zeek/Suricata)
- Management Node

Target Scale: 30+ total VMs across scenario pods.

---

## 3. Logical Network Zones

(VLANs provisioned by ECRL)

### 3.1 Student Access Zone
- VPN entry point
- Controlled RDP/SSH access

### 3.2 SOC / Monitoring Zone
- SIEM
- Log collectors
- Dashboard access

### 3.3 Enterprise Simulation Zone
- Domain controller
- Workstations
- Application servers
- File servers

### 3.4 Attacker Zone (Internal Only)
- Kali / Red Team infrastructure
- No outbound uncontrolled attack traffic

---

## 4. Telemetry Flow

Endpoint Logs (Sysmon, auditd, Windows logs)
        ↓
Forwarders / Agents
        ↓
Central SIEM
        ↓
Dashboards / Alerts / Correlation Searches

All logs must maintain synchronized time (NTP required).

---

## 5. Scenario Pod Model

Each scenario pod includes:

- Required VMs
- User accounts
- Vulnerable service or condition
- Expected attacker behavior
- Detection rules
- Reset instructions

Pods must be:

- Modular
- Documented
- Resettable
- Scalable

---

## 6. Reset Strategy

### Baseline Layer
- Clean OS images
- Minimal configuration
- Rare snapshot usage

### Scenario Layer
- Controlled misconfigurations
- Pre-built attack conditions
- Documented restore steps

Rebuild Process:
- Reinstall VM from template if required
- Restore configuration from documented scripts
- Validate telemetry flow

---

## 7. Growth Path

Phase 1: Core environment stabilization  
Phase 2: Implement 5 foundational scenarios  
Phase 3: Expand to enterprise-scale simulation  
Phase 4: Add detection engineering + correlation  
Phase 5: Faculty integration package  
Phase 6: Research expansion (AI / anomaly detection / advanced telemetry)

---

## 8. Long-Term Sustainability

The cyber range must:

- Outlive current team members
- Be fully documented
- Be reproducible
- Be maintainable by future cohorts
- Support both structured labs and open research

This document will evolve as infrastructure expands.
