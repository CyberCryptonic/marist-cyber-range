# SCN-005: Elastic Agent Health Validation

## Difficulty

Level 1

## Estimated Time

30 minutes

## Overview

This scenario validates that Elastic Agent endpoints are enrolled and healthy in the Security Onion Fleet interface.

This is a readiness scenario that should be performed before more advanced attack-to-detection exercises.

## Learning Objectives

By the end of this scenario, students should be able to:

- Check Elastic Agent health
- Identify which endpoints are enrolled
- Understand why endpoint telemetry matters
- Validate required network paths
- Document telemetry readiness

## Required Environment

| System | Role |
|---|---|
| Security Onion | Fleet and telemetry management |
| Windows Target Systems | Elastic Agent endpoints |
| Linux Target Systems | Elastic Agent or syslog endpoints |
| SOC Analyst Workstation | Analyst access system |

## Safety Notes

- This scenario does not require offensive activity.
- Do not reinstall agents unless troubleshooting requires it.
- Record agent status before making changes.

## Pre-Scenario Checklist

- [ ] Security Onion is running
- [ ] Fleet is accessible
- [ ] Target systems are powered on
- [ ] Required Security Onion ports are reachable from Target systems
- [ ] System clocks are synchronized

## Setup

1. Log into Security Onion from the SOC Analyst Workstation.
2. Open Fleet or the relevant agent management view.
3. Record the current agent list.
4. Identify healthy and unhealthy endpoints.

## Execution

Review endpoint health and confirm that expected Target systems are enrolled.

If an endpoint is unhealthy, check:

- Is the VM powered on?
- Is the network route working?
- Can the endpoint reach required Security Onion services?
- Is the Elastic Agent service running?
- Is time synchronized?

## Expected Telemetry

| Source | Expected Evidence |
|---|---|
| Security Onion Fleet | Healthy enrolled agents |
| Target Endpoint | Running Elastic Agent service |
| Network Tests | Required ports reachable |
| Analyst Notes | Endpoint health table |

## Detection Approach

Analysts should answer:

- Which endpoints are healthy?
- Which endpoints are unhealthy?
- Are any important systems missing?
- Do unhealthy systems share a common issue?
- Are firewall rules blocking required communication?
- Is time drift affecting communication?

## Evidence to Capture

- Fleet agent list screenshot
- Endpoint service status screenshot if needed
- Connectivity test screenshot if needed
- Analyst notes with endpoint health summary

## Reset Procedure

No reset should be needed.

If changes were made:

1. Restart only the affected service.
2. Confirm agent health returns.
3. Document the fix.
4. Capture evidence.

## Success Criteria

- [ ] Expected endpoints appear in Fleet
- [ ] Healthy systems are identified
- [ ] Unhealthy systems are documented
- [ ] Required telemetry path is validated
- [ ] Notes are saved for future troubleshooting
