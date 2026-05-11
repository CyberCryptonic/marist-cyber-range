# Logging Baseline

This file documents the minimum logging and telemetry expectations for systems in the Marist Cyber Range.

The goal is to make sure systems are detection-ready before scenarios are executed.

## Purpose

A cyber range is only useful for SOC training if activity can be observed.

This baseline helps future teams confirm that systems are producing useful telemetry before running attack or investigation scenarios.

## Core Telemetry Sources

| Source | Method | Destination |
|---|---|---|
| OPNsense Firewall | Syslog | Security Onion |
| Windows Endpoints | Elastic Agent / future Windows Event Forwarding | Security Onion |
| Linux Endpoints | rsyslog / Elastic Agent | Security Onion |
| Security Onion | Native sensors and ingest services | Security Onion |
| Vulnerable Applications | Application logs / Docker logs / endpoint logs | Security Onion or local validation |
| Network Traffic Generator | Network traffic and host logs | Security Onion visibility |

## Windows Logging Baseline

Windows systems should produce logs for:

- Successful logons
- Failed logons
- Account lockouts
- User creation
- Group membership changes
- Privileged logon events
- Process activity where available
- Service installation where available
- PowerShell activity where available
- System events
- Security events

Recommended Windows systems to monitor:

- Primary Domain Controller
- Backup Domain Controller
- File Server
- Internal Web Server
- Windows Log Server
- Windows 10 / Windows 11 user workstations
- IT Admin Workstation

## Linux Logging Baseline

Linux systems should produce logs for:

- Authentication attempts
- sudo usage
- SSH activity
- service starts and stops
- package installation
- cron activity
- system errors
- network service activity

Recommended Linux systems to monitor:

- Kali Purple
- Incident Response Workstation
- Vulnerable Training Server
- Network Traffic Generator
- Range Orchestration Server
- Adversary Simulation Server

## Firewall Logging Baseline

OPNsense should log:

- Allowed traffic where needed for validation
- Denied traffic for restricted paths
- Target-to-SOC telemetry flows
- Management access attempts
- Rule hits for scenario-specific firewall rules

Firewall logs should be forwarded to Security Onion using syslog.

## Security Onion Validation

Before running a scenario, confirm:

- Security Onion dashboard loads successfully
- Time is correct
- Hunt is accessible
- Fleet is accessible if Elastic Agent is in use
- Expected endpoint agents are healthy
- Firewall logs are visible
- Test events can be found

## Test Event Examples

Safe validation events:

- Failed login attempt on a test workstation
- Access to internal web server
- File share access test
- Linux `logger` test event
- Ping between approved hosts
- Low-rate connectivity test from traffic generator
- OPNsense blocked management access attempt from Target network

## Baseline Checklist

- [ ] Domain Controller logs are being generated
- [ ] Windows endpoint telemetry is active
- [ ] Linux syslog forwarding is configured where needed
- [ ] Elastic Agent status is healthy where installed
- [ ] OPNsense syslog forwarding is active
- [ ] Security Onion receives expected events
- [ ] System clocks are synchronized
- [ ] Snapshots exist before scenario execution
- [ ] Known logging gaps are documented

## Known Improvement Areas

Future teams should consider adding:

- Sysmon
- Sigma rules
- Windows Event Forwarding tuning
- Custom Security Onion detections
- Scenario-specific dashboards
- Automated telemetry validation scripts
- Case tracking workflow
- Formal SOC analyst report templates
