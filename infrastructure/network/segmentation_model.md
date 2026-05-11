# Network Segmentation Model

This file explains the segmentation design used by the Marist Cyber Range.

## Purpose

The cyber range is separated into multiple networks so students can train in an environment that feels closer to a real enterprise.

Instead of placing every VM on one flat network, the range uses logical separation between:

- Red Team systems
- Target enterprise systems
- SOC / Detection systems

This improves realism, strengthens safety, and allows scenarios to be built around traffic flow, firewall rules, and monitoring boundaries.

## Environment Zones

| Zone | Subnet | Description |
|---|---|---|
| Red Team | `10.20.10.0/24` | Offensive systems used for controlled attacker activity |
| Target | `10.20.20.0/24` | Domain-joined enterprise victim systems |
| SOC / Detection | `10.20.30.0/24` | Security Onion, SOC workstations, firewall management, and detection tools |

## Firewall Role

OPNsense is used as the active firewall and segmentation system between the Target and SOC environments.

The firewall supports:

- Routing between selected networks
- Firewall rule enforcement
- Management access restriction
- Syslog forwarding to Security Onion
- Segmentation validation
- Future traffic control for scenarios

## Segmentation Goals

The segmentation model was designed to enforce these goals:

1. Target systems should not freely manage SOC systems.
2. SOC systems should be able to monitor and administer approved infrastructure.
3. Firewall management should be restricted to SOC-side systems.
4. Security Onion should receive logs and telemetry from approved sources.
5. Red Team activity should be controlled and observable.
6. Future scenarios should be able to use firewall rules as part of the learning objective.

## Example Traffic Flows

| Source | Destination | Purpose |
|---|---|---|
| Target systems | Security Onion | Elastic Agent, syslog, telemetry forwarding |
| OPNsense | Security Onion | Firewall syslog forwarding |
| SOC Analyst Workstations | Security Onion | Analyst dashboard access |
| SOC Analyst Workstations | OPNsense | Firewall management |
| Target systems | Internal Web Server | Normal enterprise web access |
| Target users | File Server | Department share access |
| Red Team systems | Target systems | Controlled scenario execution |

## Restricted Traffic

The following traffic should generally be restricted unless a scenario requires it:

| Source | Destination | Reason |
|---|---|---|
| Target systems | OPNsense web GUI | Prevent normal users from managing the firewall |
| Target systems | SOC workstations | Protect monitoring and analyst systems |
| Red Team systems | SOC systems | Prevent attackers from directly targeting SOC tooling unless specifically planned |
| Student endpoints | Infrastructure management interfaces | Preserve administrative boundaries |

## Security Onion Visibility

Security Onion should receive telemetry from:

- OPNsense firewall logs
- Elastic Agent endpoints
- Linux syslog sources
- Network traffic visible through the monitoring interface
- Future Windows Event Forwarding or Sysmon sources

## Validation Checklist

Use this checklist after major network changes:

- [ ] Target systems can reach required internal services
- [ ] Target systems can reach Security Onion Fleet / Elastic services if Elastic Agent is used
- [ ] OPNsense can forward logs to Security Onion
- [ ] SOC workstations can access Security Onion
- [ ] SOC workstations can manage OPNsense
- [ ] Target systems cannot access firewall management
- [ ] Red Team traffic is controlled and expected
- [ ] Security Onion receives expected telemetry after test events
- [ ] Time synchronization is stable across monitored systems

## Notes

The segmentation model should be reviewed before every new scenario is added. If a scenario requires new communication paths, the firewall rule should be documented and later removed or disabled if it is not needed permanently.
