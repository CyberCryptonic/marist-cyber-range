# SCN-002: Failed Logon Triage

## Difficulty

Level 1

## Estimated Time

30-45 minutes

## Overview

This scenario teaches students how to investigate repeated failed logon activity.

The activity is generated using a test account inside the Target Environment. SOC analysts review Windows logs, endpoint telemetry, and Security Onion data to understand what happened.

## Learning Objectives

By the end of this scenario, students should be able to:

- Identify failed authentication activity
- Understand why failed logons matter in SOC investigations
- Review Windows event evidence
- Correlate username, source host, and time
- Document whether activity appears expected or suspicious

## Required Environment

| System | Role |
|---|---|
| Domain Controller | Authentication source |
| Windows Workstation | System where failed login attempts are generated |
| Security Onion | Central review platform |
| SOC Analyst Workstation | Analyst access system |

## Safety Notes

- Use only lab-created accounts.
- Do not use real user passwords.
- Do not lock out important administrative accounts.
- Keep attempts limited and controlled.

## Pre-Scenario Checklist

- [ ] Domain Controller is running
- [ ] Test user account exists
- [ ] Windows workstation is domain joined
- [ ] Security Onion is running
- [ ] Endpoint telemetry is active where available
- [ ] Time is synchronized

## Setup

1. Select a non-critical test user account.
2. Confirm the account is not used for infrastructure administration.
3. Record the workstation name and IP address.
4. Record the start time.

## Execution

Generate a small number of failed login attempts using the test account on an approved lab workstation.

Do not generate excessive attempts.

## Expected Telemetry

| Source | Expected Evidence |
|---|---|
| Domain Controller | Failed authentication events |
| Windows Workstation | Local logon failure evidence |
| Security Onion | Endpoint or authentication-related telemetry, depending on ingestion |
| Analyst Notes | Username, source system, timestamp, and event summary |

## Detection Approach

Analysts should answer:

- Which user account was involved?
- Which workstation generated the failed attempts?
- What time did the attempts occur?
- Were the attempts repeated?
- Was the account locked out?
- Did the activity appear accidental, expected, or suspicious?
- What evidence supports the conclusion?

## Evidence to Capture

- Windows Event Viewer screenshot
- Security Onion screenshot, if telemetry is available
- Timeline of failed attempts
- Analyst conclusion

## Reset Procedure

1. Stop failed logon attempts.
2. Unlock the test account if needed.
3. Confirm the account is usable.
4. Save evidence.
5. Document any logging gaps.

## Success Criteria

- [ ] Failed logon activity was generated safely
- [ ] Relevant authentication evidence was found
- [ ] Source workstation was identified
- [ ] Username was identified
- [ ] Analyst notes were completed
- [ ] Test account was returned to normal
