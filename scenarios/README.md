# Scenarios

This folder contains scenario playbooks for the Marist Cyber Range.

Each scenario should follow the same structure:

`setup → execution → expected telemetry → detection → evidence → reset`

## Purpose

The cyber range was built to support realistic cybersecurity training.

Scenarios give students a structured way to:

- Generate controlled activity
- Observe how activity appears in logs
- Practice SOC triage
- Identify useful telemetry
- Document findings
- Understand logging gaps
- Reset the environment safely

## Scenario Format

Each scenario should include:

| Section | Purpose |
|---|---|
| Overview | What the scenario teaches |
| Learning Objectives | What students should understand after completing it |
| Environment | Required VMs and subnets |
| Safety Notes | Boundaries and restrictions |
| Setup | What must be ready before execution |
| Execution | High-level steps for running the scenario |
| Expected Telemetry | Logs, alerts, and network activity that should appear |
| Detection Approach | How analysts should investigate |
| Evidence to Capture | Screenshots, log entries, dashboards, and notes |
| Reset Procedure | How to return the environment to a clean state |
| Success Criteria | How to know the scenario worked |

## Scenario Difficulty Levels

| Level | Meaning |
|---|---|
| Level 1 | Basic validation or beginner SOC investigation |
| Level 2 | Multi-system investigation with clear telemetry |
| Level 3 | More realistic investigation requiring correlation |
| Level 4 | Advanced scenario with multiple stages |
| Level 5 | Capstone scenario requiring full attack-to-detection workflow |

## Initial Scenario Library

Recommended starter scenarios:

| Scenario ID | Name | Purpose |
|---|---|---|
| `SCN-001` | Port Scan Detection | Detect and investigate network reconnaissance |
| `SCN-002` | Failed Logon Triage | Investigate repeated failed authentication attempts |
| `SCN-003` | Firewall Denied Management Access | Validate segmentation and firewall visibility |
| `SCN-004` | Vulnerable Web App Traffic | Observe web application traffic against vulnerable services |
| `SCN-005` | Elastic Agent Health Validation | Confirm endpoint telemetry health |
| `SCN-006` | File Share Access Validation | Validate role-based file share access and evidence collection |

## Evidence Expectations

Each scenario should include screenshots or evidence from:

- Security Onion Hunt
- Security Onion Alerts, if applicable
- Fleet / Elastic Agent health, if applicable
- OPNsense logs, if applicable
- Windows Event Viewer, if applicable
- Linux logs, if applicable
- Terminal output from test systems
- Relevant VM status in Proxmox

## Responsible Use

All scenarios are designed for the isolated Marist Cyber Range.

Do not run offensive tools, scans, traffic generation, or adversary simulation outside an authorized lab environment.

## Notes for Future Teams

Future teams should continue expanding this folder with:

- Full attack-to-detection scenarios
- MITRE ATT&CK mapping
- Detection engineering exercises
- Sigma rule testing
- Caldera-based operations
- SOC case-tracking workflows
- Student handouts
- Instructor answer keys
