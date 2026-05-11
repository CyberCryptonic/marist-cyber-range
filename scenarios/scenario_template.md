# Scenario Template

## Scenario ID

`SCN-XXX`

## Scenario Name

`Replace with scenario name`

## Difficulty

Level: `1-5`

## Estimated Time

`Replace with estimated completion time`

## Overview

Describe what the scenario is designed to teach.

## Learning Objectives

By the end of this scenario, students should be able to:

- Objective 1
- Objective 2
- Objective 3

## Required Environment

| System | Role |
|---|---|
| System name | Purpose |
| System name | Purpose |

## Required Tools

List the tools required for the scenario.

Examples:

- Security Onion
- OPNsense
- Elastic Agent
- Windows Event Viewer
- Linux terminal
- tcpdump
- Wireshark
- Kali Linux
- MITRE Caldera

## Safety Notes

- Run this scenario only inside the isolated cyber range.
- Confirm snapshots exist before beginning.
- Do not run offensive activity against systems outside the lab.
- Use rate limits for traffic generation.
- Document any system changes.

## Pre-Scenario Checklist

- [ ] Security Onion is running
- [ ] Required VMs are powered on
- [ ] System clocks are synchronized
- [ ] Required agents/logging services are active
- [ ] Snapshots exist
- [ ] Firewall rules are in the expected state
- [ ] Analyst workstation can access Security Onion

## Setup

Document any setup required before execution.

## Execution

Document the controlled activity that will be performed.

Keep this section safe, authorized, and scoped to the cyber range.

## Expected Telemetry

| Source | Expected Evidence |
|---|---|
| Security Onion | Expected event or search result |
| OPNsense | Expected firewall log |
| Windows Event Logs | Expected Windows event |
| Linux Logs | Expected Linux log |
| Endpoint Agent | Expected host telemetry |

## Detection Approach

Explain how an analyst should investigate the scenario.

Include suggested questions:

- What system generated the event?
- What user account was involved?
- What destination was contacted?
- Was the activity expected?
- What logs confirm the event?
- What logs are missing?
- Should this be escalated?

## Evidence to Capture

- Screenshot 1
- Screenshot 2
- Log entry
- Analyst notes
- Timeline of activity

## Reset Procedure

Explain how to return the environment to a normal state.

## Success Criteria

The scenario is complete when:

- [ ] Expected activity was generated
- [ ] Expected telemetry was found
- [ ] Evidence was captured
- [ ] Analyst notes were completed
- [ ] Environment was reset
