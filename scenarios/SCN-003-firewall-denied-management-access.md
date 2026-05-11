# SCN-003: Firewall Denied Management Access

## Difficulty

Level 1

## Estimated Time

20-30 minutes

## Overview

This scenario validates segmentation between the Target Environment and SOC / Detection Environment.

A Target-side system attempts to access a firewall management interface that should only be reachable from approved SOC systems. Analysts review firewall logs and Security Onion telemetry to confirm the attempted access was denied or restricted.

## Learning Objectives

By the end of this scenario, students should be able to:

- Explain why management interfaces should be restricted
- Validate firewall segmentation
- Review OPNsense firewall logs
- Search Security Onion for firewall telemetry
- Document blocked access attempts

## Required Environment

| System | Role |
|---|---|
| Target Workstation | Attempts restricted access |
| OPNsense | Firewall and segmentation enforcement |
| Security Onion | Log review |
| SOC Analyst Workstation | Analyst access system |

## Safety Notes

- This scenario should only test access to the lab firewall.
- Do not attempt to bypass authentication.
- Do not modify firewall rules during the scenario unless directed by the instructor.
- Use only approved Target systems.

## Pre-Scenario Checklist

- [ ] OPNsense is running
- [ ] Firewall management is restricted to SOC systems
- [ ] Security Onion is receiving OPNsense logs
- [ ] Target workstation is online
- [ ] SOC analyst workstation can access Security Onion
- [ ] Time is synchronized

## Setup

1. Confirm the OPNsense management IP.
2. Confirm the Target workstation IP.
3. Confirm the SOC workstation can access the firewall management page.
4. Confirm the Target workstation should not be allowed to manage the firewall.

## Execution

From an approved Target workstation, attempt to reach the firewall management interface.

This test should validate that firewall management is restricted.

## Expected Telemetry

| Source | Expected Evidence |
|---|---|
| OPNsense | Blocked or denied access attempt from Target subnet |
| Security Onion | Firewall log event if syslog forwarding is active |
| Target Workstation | Browser or connection failure |
| Analyst Notes | Source IP, destination IP, time, and result |

## Detection Approach

Analysts should answer:

- Which host attempted access?
- Which firewall interface was targeted?
- Was the attempt allowed or denied?
- Did the firewall rule behave as expected?
- Was the event visible in Security Onion?
- Does this confirm segmentation is working?

## Evidence to Capture

- Target workstation screenshot showing failed access
- OPNsense firewall log screenshot
- Security Onion Hunt screenshot showing firewall event
- Analyst notes

## Reset Procedure

No system reset should be required.

1. Close the browser or connection attempt.
2. Confirm firewall rules were not changed.
3. Save evidence.
4. Document results.

## Success Criteria

- [ ] Target system could not manage OPNsense
- [ ] SOC system could still manage OPNsense
- [ ] OPNsense logged the attempt
- [ ] Security Onion displayed the event if forwarding was active
- [ ] Segmentation was validated
