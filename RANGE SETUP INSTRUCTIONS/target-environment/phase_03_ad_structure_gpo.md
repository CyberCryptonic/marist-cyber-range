## Status

🚧 Nearly Complete

- Users created  
- Groups implemented  
- GPO deployed  
- Audit logging enabled  
- Minor OU cleanup and validation remaining  

---

# Marist SOC Cyber Range  
# Lab Build Guide — Phase 03: Active Directory Structure, Users, Groups, and Group Policy

---

# Purpose

Phase 03 transforms the cyber range from a basic Active Directory deployment into a structured, enterprise-managed environment.

This phase introduces:

- Organizational structure (OUs)  
- Identity management (users)  
- Role-based access control (groups)  
- Centralized configuration (Group Policy)  
- Security visibility (audit logging)  

By completing this phase, the environment behaves like a real enterprise network and becomes ready for both defensive (SOC) and offensive (Red Team) operations.

---

# Objectives

- Create Organizational Units (OUs)  
- Create users and security groups  
- Assign group memberships  
- Organize computers into OUs  
- Deploy Group Policy Objects (GPOs)  
- Enable audit logging  
- Validate policy enforcement  

---

# Prerequisites

- Proxmox environment operational  
- Domain Controller (Windows Server 2022) configured  
- Domain: cyberrange.local  
- Windows 10 and Windows 11 systems joined to domain  
- Domain authentication functioning  

---

# Target Active Directory Structure

```
cyberrange.local
│
├── Employees
├── IT
├── Servers
├── Workstations
├── Groups
```

---

# Part 1 — Create Organizational Units (OUs)

## Step 1

On Domain Controller:

Open:
Active Directory Users and Computers  

Expand:
cyberrange.local  

---

## Step 2

Right-click domain → New → Organizational Unit  

Create:

- Employees  
- IT  
- Servers  
- Workstations  
- Groups  

---

# Part 2 — Create Users

## Step 3 — Employee Users

Navigate to:
Employees OU  

Right-click → New → User  

Create:

- jdoe  
- jsmith  
- mjones  

Set password:

Cyberrange2026  

Configure:

- Disable: User must change password  
- Enable: Password never expires  

---

## Step 4 — Admin User

Navigate to:
IT OU  

Create:

- itadmin  

---

# Part 3 — Create Security Groups

## Step 5

Navigate to:
Groups OU  

Create:

- IT-Admins  
- Employees  

---

## Step 6 — Assign Group Membership

### IT-Admins Group

Add:

- itadmin  

---

### Employees Group

Add:

- jdoe  
- jsmith  
- mjones  

---

# Part 4 — Organize Computers

## Step 7

Navigate to:
Computers container  

Locate all domain-joined systems:

- Windows 10 machines  
- Windows 11 machines  

Right-click → Move  

Move to:

Workstations OU  

---

# Part 5 — Verify Administrative Access

## Step 8

Log into a workstation:

CYBERRANGE\itadmin  

---

## Step 9

Open Command Prompt (Admin)  

Run:

whoami /groups  

Verify membership includes:

- IT-Admins  
- Domain Admins  

---

# Part 6 — Create Group Policy

## Step 10

On Domain Controller:

Run:

gpmc.msc  

---

## Step 11

Navigate:

cyberrange.local → Workstations OU  

Right-click:

Create a GPO in this domain, and link it here  

Name:

Workstation-Baseline-GPO  

---

## Step 12

Right-click GPO → Edit  

---

# Part 7 — Configure Audit Policy

Navigate:

Computer Configuration  
→ Policies  
→ Windows Settings  
→ Security Settings  
→ Advanced Audit Policy Configuration  
→ Audit Policies  

---

## Step 13 — Enable Logging

### Account Logon
- Credential Validation → Success, Failure  

### Account Management
- User Account Management → Success, Failure  
- Security Group Management → Success, Failure  

### Logon/Logoff
- Logon → Success, Failure  
- Logoff → Success  

### Privilege Use
- Sensitive Privilege Use → Success, Failure  

### System
- System Integrity → Success, Failure  

---

# Part 8 — Enable Remote Desktop

Navigate:

Computer Configuration  
→ Administrative Templates  
→ Windows Components  
→ Remote Desktop Services  
→ Remote Desktop Session Host  
→ Connections  

Enable:

Allow users to connect remotely using Remote Desktop Services  

---

# Part 9 — Apply Group Policy

## Step 14 — All Workstations

Open Command Prompt (Admin)  

Run:

gpupdate /force  

Restart system  

---

# Part 10 — Verify GPO Application

## Step 15

On a workstation, run:

gpresult /r  

---

## Step 16 — Verify Output

Under COMPUTER SETTINGS confirm:

- Workstation-Baseline-GPO  
- Default Domain Policy  

---

# Part 11 — Validate Logging

## Step 17 — Generate Activity

- Log out  
- Attempt failed login  
- Log in successfully  

---

## Step 18

Open:

Event Viewer  
→ Windows Logs  
→ Security  

---

## Step 19 — Verify Events

Confirm presence of:

- 4624 — Successful logon  
- 4634 — Logoff  
- 4672 — Privileged logon  
- 5379 — Credential activity  

---

# Expected Results

- Active Directory structure fully organized  
- Users and groups created and assigned  
- Workstations properly placed in correct OU  
- GPO successfully applied and enforced  
- Policies visible in gpresult  
- Audit logs actively generated  
- Domain environment behaves like enterprise network  

---

# Key Concepts

- OUs define structure and policy scope  
- Groups enforce role-based access control  
- GPO provides centralized configuration management  
- gpresult verifies policy application  
- Event Viewer provides security visibility  

---

# Common Mistakes

- Not linking GPO to correct OU  
- Not restarting machines after gpupdate  
- Misplacing computers outside intended OU  
- Not running gpresult as administrator  
- Assuming GPO applies without validation  

---

# Current Environment State

At this stage:

- Users and groups are fully implemented  
- GPO is deployed and functioning  
- Audit logging is active  
- Domain environment is operational  

Remaining work:

- OU cleanup and refinement  
- Group validation  
- Final permission alignment  

---

# Phase Completion Criteria

Phase 03 is complete when:

- OUs are fully structured  
- Users and groups are properly assigned  
- Machines are placed in correct OU  
- GPO is created, linked, and applied  
- GPO appears in gpresult  
- Security logs are consistently generated  

---

# Transition to Phase 04

Next phase:

- File server deployment  
- Shared folder structure  
- Access control using AD groups  
- Permission enforcement  

---

# Summary

Phase 03 establishes centralized identity, access control, and policy enforcement across the cyber range.

This phase marks the transition from a simple domain environment to a fully managed enterprise system, enabling realistic user behavior, controlled access to resources, and SOC-ready logging and visibility.
