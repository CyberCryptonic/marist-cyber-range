# Infrastructure

This directory contains automation, configuration references, network design material, provisioning notes, and baseline documentation for the Marist SOC Cyber Range.

The goal of this folder is to support repeatable builds, standardized configurations, future automation, and Infrastructure-as-Code style workflows.

## Purpose

The Marist Cyber Range was built as a segmented virtual enterprise environment hosted on Proxmox.

The infrastructure folder documents the technical foundation that supports:

- Repeatable environment builds
- Standardized VM configuration
- Network segmentation
- IP addressing
- Firewall and routing design
- Logging readiness
- Endpoint telemetry readiness
- Future automation
- Future orchestration
- Future Infrastructure-as-Code development

This folder does not replace the full step-by-step build guides in `RANGE SETUP INSTRUCTIONS/`.

Instead, it acts as the reusable technical reference layer for future teams.

## Recommended Folder Structure

| Folder | Purpose |
|---|---|
| `scripts/` | Automation scripts for configuring systems |
| `configs/` | Static configuration files and exported configuration references |
| `network/` | IP addressing, subnet design, segmentation notes, and firewall logic |
| `provisioning/` | VM specifications, build order, template strategy, and deployment logic |
| `baselines/` | Logging, security, and detection-ready baseline notes |

## Current Environment Summary

The cyber range is organized into three main environments.

| Environment | Subnet | Purpose |
|---|---|---|
| Red Team Environment | `10.20.10.0/24` | Offensive activity, attacker systems, instructor systems |
| Target Environment | `10.20.20.0/24` | Enterprise victim network with AD, users, servers, web services, and vulnerable apps |
| SOC / Detection Environment | `10.20.30.0/24` | Security Onion, analyst workstations, firewall management, detection and monitoring |

## Core Design Principles

The infrastructure was designed around the following principles:

1. **Segmentation**
   - Red Team, Target, and SOC networks are separated into different subnets.
   - Firewall rules control which systems can communicate.

2. **Repeatability**
   - VM templates are used where possible.
   - Build phases are documented so future teams can rebuild the environment.

3. **Visibility**
   - Target systems are configured to produce logs.
   - Security Onion receives telemetry from firewall, Linux systems, and Elastic Agent endpoints.

4. **Realism**
   - The Target Environment includes Active Directory, domain users, file shares, internal web services, admin workstations, and vulnerable applications.

5. **Safe Testing**
   - Offensive tooling is used only inside the isolated cyber range.
   - Snapshots and backups are used before major changes or scenario execution.

6. **Future Automation**
   - The folder structure is prepared for scripts, configuration exports, Ansible, provisioning logic, and baseline states.

## Files to Add First

Recommended first files for this folder:

| File | Purpose |
|---|---|
| `network/ip_allocation.md` | Documents all major subnets, gateways, and important host addresses |
| `network/segmentation_model.md` | Explains how Red Team, Target, and SOC networks are separated |
| `provisioning/vm_inventory.md` | Lists cyber range VM roles and purpose |
| `provisioning/build_order.md` | Explains the order future teams should rebuild systems |
| `baselines/logging_baseline.md` | Documents minimum logging and telemetry expectations |
| `scripts/README.md` | Explains how future scripts should be stored and documented |

## Notes for Future Teams

Future teams should use this folder when they begin automating the cyber range.

Possible future improvements:

- Ansible playbooks for Linux configuration
- PowerShell scripts for Active Directory user and group creation
- GPO backup exports
- Sysmon configuration
- Security Onion ingest validation scripts
- Elastic Agent health checks
- OPNsense configuration exports
- VM cloning scripts
- Scenario reset scripts
- Automated traffic generation scripts

This folder should gradually evolve from documentation into a true infrastructure automation libr
