# Infrastructure

This directory contains automation, configurations, and build logic for the Marist SOC Cyber Range.

The goal of this section is to support:
- Repeatable environment builds
- Standardized configurations
- Future automation (IaC-style workflows)

---

## Structure

### scripts/
Automation scripts for configuring systems

Examples:
- Active Directory user/group creation
- Endpoint configuration scripts
- Logging enablement scripts

---

### configs/
Static configuration files

Examples:
- GPO exports
- Sysmon configs (future)
- Security baselines

---

### network/
Network design and configuration

Examples:
- Subnet definitions
- IP allocation plans
- OPNsense configuration notes

---

### provisioning/
Environment build and deployment logic

Examples:
- VM specifications (CPU/RAM/storage)
- Template cloning strategy
- Build order for environments

---

### baselines/
Security and system baseline configurations

Examples:
- Windows hardening
- Logging configurations
- Detection-ready system states

---

## Purpose

This folder enables future teams to:
- Rebuild the environment from scratch
- Understand how systems were configured
- Transition toward automation and Infrastructure-as-Code practices
