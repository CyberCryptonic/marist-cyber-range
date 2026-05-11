# SCN-001: Port Scan Detection

## Difficulty

Level 1

## Estimated Time

30-45 minutes

## Overview

This scenario introduces students to network reconnaissance detection.

A controlled scan is performed from an authorized lab system against an internal target. SOC analysts then review Security Onion and firewall telemetry to identify the source, destination, timing, and possible purpose of the activity.

## Learning Objectives

By the end of this scenario, students should be able to:

- Recognize basic reconnaissance activity
- Identify source and destination IP addresses
- Use Security Onion Hunt to search for network activity
- Review firewall logs for related traffic
- Document a simple SOC investigation

## Required Environment

| System | Role |
|---|---|
| Kali Linux attacker system | Generates controlled reconnaissance traffic |
| Internal Web Server or Vulnerable Training Server | Target system |
| Security Onion | Detection and log review |
| OPNsense | Firewall visibility and segmentation logs |
| SOC Analyst Workstation | Analyst access system |

## Safety Notes

- Run only inside the isolated cyber range.
- Use low-rate scanning only.
- Do not scan external networks.
- Confirm snapshots exist before beginning.
- Stop the activity immediately if unexpected instability occurs.

## Pre-Scenario Checklist

- [ ] Security Onion dashboard is reachable
- [ ] Target system is powered on
- [ ] Attacker system is powered on
- [ ] OPNsense is logging
- [ ] Time is synchronized
- [ ] Snapshots exist

## Setup

1. Confirm the target IP address.
2. Confirm the attacker IP address.
3. Confirm Security Onion is receiving firewall or network telemetry.
4. Record the start time of the test.

## Execution

Perform a controlled, low-rate reconnaissance test from the authorized attacker VM against the approved target VM.

Keep the scan limited to the target host used for the scenario.

## Expected Telemetry

| Source | Expected Evidence |
|---|---|
| Security Onion | Network connection events involving attacker and target |
| OPNsense | Allowed or denied connection attempts depending on firewall path |
| Target Host | Possible local connection logs depending on service configuration |
| Analyst Notes | Timeline showing when activity began and ended |

## Detection Approach

Analysts should answer:

- What was the source IP?
- What was the destination IP?
- What ports or services were contacted?
- Was the activity allowed or blocked?
- Did Security Onion show related events?
- Did the firewall show related logs?
- Was the activity expected for the scenario?

## Evidence to Capture

- Security Onion Hunt screenshot showing attacker-to-target traffic
- OPNsense firewall log screenshot, if available
- Terminal screenshot showing controlled activity start time
- Analyst notes with source, destination, and timeline

## Reset Procedure

1. Stop the scan or test activity.
2. Confirm the target system is still responsive.
3. Confirm Security Onion remains healthy.
4. Save evidence screenshots.
5. Record any issues found during the scenario.

## Success Criteria

- [ ] Controlled reconnaissance traffic was generated
- [ ] Security Onion showed related network activity
- [ ] Firewall logs were reviewed
- [ ] Source and destination were identified
- [ ] Evidence was captured
- [ ] Environment remained stable
