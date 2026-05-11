# Build Order

This file documents the recommended build order for recreating the Marist Cyber Range.

The detailed step-by-step instructions are stored in `RANGE SETUP INSTRUCTIONS/`. This file provides the high-level rebuild sequence.

## Build Philosophy

The cyber range should be built from the foundation upward.

Recommended order:

1. Virtualization platform
2. Network bridges and segmentation
3. Target Environment core services
4. Red Team Environment
5. SOC / Detection Environment
6. Logging and telemetry
7. Vulnerable services
8. Scenarios
9. Backups and snapshots

## Phase 1: Proxmox Foundation

Build or validate:

- Proxmox VE host
- Storage configuration
- Network bridges
- ISO storage
- VM templates
- Backup storage
- Snapshot strategy

Validation:

- [ ] Proxmox web interface is reachable
- [ ] Network bridges are present
- [ ] Templates are available
- [ ] VM storage is healthy
- [ ] Backup location is available

## Phase 2: Target Network Foundation

Build:

- Target subnet
- Primary Domain Controller
- DNS
- Active Directory domain
- Backup Domain Controller
- Domain-joined endpoints

Validation:

- [ ] Domain exists
- [ ] DNS resolution works
- [ ] Endpoints can join the domain
- [ ] Domain users can authenticate
- [ ] Time synchronization is stable

## Phase 3: Target Enterprise Services

Build:

- Active Directory OUs
- Users and groups
- Group Policy structure
- File Server
- Department shares
- Internal Web Server
- Windows Log Server preparation
- IT Admin Workstation
- Incident Response Workstation
- Kali Purple Workstation
- Vulnerable Training Server

Validation:

- [ ] File shares enforce role-based access
- [ ] Internal website is reachable
- [ ] Admin workstation can manage domain tools
- [ ] Vulnerable applications are reachable
- [ ] Logging policies are applied

## Phase 4: Red Team Environment

Build:

- Student Kali attacker systems
- Instructor attacker system
- Red Team jump server
- Red Team subnet

Validation:

- [ ] Red Team systems boot successfully
- [ ] Tools are available
- [ ] Red Team traffic is isolated and controlled
- [ ] Red Team systems can reach only approved targets

## Phase 5: SOC / Detection Environment

Build:

- Security Onion
- SOC Analyst Workstations
- OPNsense firewall
- Firewall rules and aliases
- Syslog forwarding
- Adversary Simulation Server
- MITRE Caldera
- Range Orchestration Server
- Core Network Router staging

Validation:

- [ ] Security Onion dashboard is reachable
- [ ] SOC workstations can access Security Onion
- [ ] OPNsense GUI is reachable from SOC systems
- [ ] Target systems cannot manage OPNsense
- [ ] OPNsense logs appear in Security Onion
- [ ] Elastic Agent systems enroll successfully
- [ ] Linux syslog traffic reaches Security Onion
- [ ] Caldera is reachable in the lab

## Phase 6: Telemetry and Detection Readiness

Configure:

- Elastic Agent on Windows and Linux endpoints
- Fleet policy for Target Environment
- Linux rsyslog forwarding
- Firewall syslog forwarding
- Security Onion allowlists
- Time synchronization
- Test event generation

Validation:

- [ ] Elastic Agent endpoints are healthy
- [ ] OPNsense logs appear in Security Onion
- [ ] Linux test logs are forwarded
- [ ] Security Onion Hunt can locate expected events
- [ ] Time stamps align across systems

## Phase 7: Backup and Snapshot

Before scenarios:

- Create clean snapshots
- Create full backups
- Document restore points

Validation:

- [ ] Snapshot exists for each critical VM
- [ ] Backup exists for each critical VM
- [ ] Restore process has been tested on at least one VM
- [ ] Backups are clearly named

## Phase 8: Scenario Readiness

Before running scenarios:

- Confirm all systems are powered on
- Confirm Security Onion is healthy
- Confirm firewall rules are correct
- Confirm telemetry sources are active
- Confirm snapshots exist
- Confirm reset steps are documented

## Notes

Future teams should not begin offensive scenarios until the environment is backed up and telemetry has been validated.

