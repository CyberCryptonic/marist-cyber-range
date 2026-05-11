# SCN-006: File Share Access Validation

## Difficulty

Level 1

## Estimated Time

30-45 minutes

## Overview

This scenario validates role-based access control for department file shares in the Target Environment.

Students test approved and denied access paths using domain accounts, then document the results and available evidence.

## Learning Objectives

By the end of this scenario, students should be able to:

- Explain role-based access control
- Validate department share permissions
- Identify expected access versus denied access
- Capture evidence of file server access behavior
- Understand how file access can support future data-focused scenarios

## Required Environment

| System | Role |
|---|---|
| File Server | Hosts department shares |
| Domain Controller | Provides authentication and group membership |
| Windows Workstation | Used to test user access |
| Security Onion | Optional telemetry review |
| SOC Analyst Workstation | Optional analyst review |

## Safety Notes

- Use only lab-created test accounts.
- Do not modify production-style shared files unless the scenario requires it.
- Do not change permissions during the scenario unless directed.
- Restore any modified files after testing.

## Pre-Scenario Checklist

- [ ] File Server is online
- [ ] Domain Controller is online
- [ ] Test accounts exist
- [ ] Group memberships are configured
- [ ] Department shares are reachable
- [ ] Snapshots exist

## Setup

1. Select test users from different departments.
2. Confirm expected group memberships.
3. Identify which shares should be allowed.
4. Identify which shares should be denied.
5. Record the start time.

## Execution

From a domain-joined workstation, test access to department shares using approved lab accounts.

Examples:

- HR user attempts HR share access
- HR user attempts IT share access
- IT user attempts IT share access
- Student user attempts Public share access
- Student user attempts restricted department share access

## Expected Telemetry

| Source | Expected Evidence |
|---|---|
| File Server | Access success or failure evidence |
| Windows Workstation | Access denied or successful file browsing |
| Domain Controller | Authentication-related events |
| Security Onion | Endpoint telemetry if configured |
| Analyst Notes | User, share, result, timestamp |

## Detection Approach

Analysts should answer:

- Which user account was tested?
- Which share was accessed?
- Was access allowed or denied?
- Did the result match the expected permission model?
- Was there evidence in Windows logs?
- Was there evidence in Security Onion?
- Are permissions configured correctly?

## Evidence to Capture

- Screenshot of successful access
- Screenshot of denied access
- Group membership screenshot if needed
- File Server or Windows event evidence if available
- Analyst notes table

## Reset Procedure

1. Log out of test accounts.
2. Remove any test files created during validation.
3. Confirm permissions were not changed.
4. Save evidence.
5. Document any permission issues.

## Success Criteria

- [ ] Approved users accessed expected shares
- [ ] Unauthorized users were denied from restricted shares
- [ ] Results were documented
- [ ] Evidence was captured
- [ ] No unintended permission changes were made
