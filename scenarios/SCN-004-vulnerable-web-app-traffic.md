# SCN-004: Vulnerable Web App Traffic

## Difficulty

Level 2

## Estimated Time

45-60 minutes

## Overview

This scenario introduces web application traffic monitoring using intentionally vulnerable applications hosted inside the cyber range.

Students generate normal web browsing activity against the vulnerable training server, then review telemetry in Security Onion and related logs.

This scenario is focused on visibility and traffic analysis, not exploitation.

## Learning Objectives

By the end of this scenario, students should be able to:

- Identify web traffic between a client and internal server
- Recognize HTTP service access in logs
- Review source and destination information
- Capture evidence of web application activity
- Understand how vulnerable apps support future attack-to-detection scenarios

## Required Environment

| System | Role |
|---|---|
| Vulnerable Training Server | Hosts DVWA, Juice Shop, or other training applications |
| Target Workstation or Kali system | Generates approved web traffic |
| Security Onion | Network and telemetry review |
| SOC Analyst Workstation | Analyst access system |

## Safety Notes

- Use only the vulnerable applications inside the lab.
- Do not target public web applications.
- This scenario should focus on browsing and visibility validation.
- Do not perform destructive web attacks.

## Pre-Scenario Checklist

- [ ] Vulnerable Training Server is online
- [ ] Docker containers are running if required
- [ ] Web application ports are reachable
- [ ] Security Onion is online
- [ ] Time is synchronized
- [ ] Snapshots exist

## Setup

1. Confirm the vulnerable server IP address.
2. Confirm which application is running.
3. Confirm the application is reachable from a test system.
4. Record the start time.

## Execution

Generate normal web browsing traffic to the approved vulnerable application.

Examples of safe activity:

- Open the homepage
- Navigate through several pages
- Log in with lab-provided test credentials if applicable
- Load static content
- Submit basic non-sensitive test forms if the app supports it

## Expected Telemetry

| Source | Expected Evidence |
|---|---|
| Security Onion | HTTP or network connection events |
| Vulnerable Server | Web server or container logs |
| Client System | Browser history or terminal output if using curl |
| Analyst Notes | Source IP, destination IP, URL path if visible, timestamp |

## Detection Approach

Analysts should answer:

- Which client accessed the web application?
- Which server and port were contacted?
- What time did the activity occur?
- Was the traffic normal browsing or suspicious?
- Were URL paths visible?
- What additional logs would improve the investigation?

## Evidence to Capture

- Web application screenshot
- Security Onion screenshot showing web traffic
- Server-side log screenshot if available
- Analyst notes with source, destination, and timeline

## Reset Procedure

1. Stop browsing activity.
2. Confirm the web application remains available.
3. Restart containers only if needed.
4. Save evidence.
5. Document any visibility gaps.

## Success Criteria

- [ ] Web application traffic was generated
- [ ] Security Onion showed related network activity
- [ ] Server was reachable
- [ ] Source and destination were identified
- [ ] Evidence was captured
- [ ] No destructive testing was performed
