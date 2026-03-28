## Status

🚧 Nearly Complete

- Users created
- Groups implemented
- GPO deployed
- Logging enabled
- Minor cleanup remaining

# Marist SOC Cyber Range  
## Phase 03 — Active Directory Structure, Users, Groups, and Group Policy

---

# Overview

Phase 03 transforms a basic Active Directory deployment into a structured and managed enterprise environment. This includes organizing directory objects, implementing access control via groups, and enforcing centralized policy using Group Policy Objects (GPOs).

By completing this phase, the environment will support:

- Structured identity management
- Role-based access control
- Centralized endpoint configuration
- Security auditing and logging

This phase is critical because it introduces the control and visibility required for both defensive (SOC) and offensive (Red Team) operations later in the project.

---

# Lab Objectives

- Create Organizational Units (OUs)
- Create users and security groups
- Assign group memberships
- Organize computers into OUs
- Create and apply Group Policy
- Enable audit logging
- Validate policy enforcement

---

# Prerequisites

- Proxmox environment running
- Domain Controller (Windows Server 2022) configured
- Domain: cyberrange.local
- Windows 10 and Windows 11 joined to domain
- Domain login working

---

# Target AD Structure

cyberrange.local
│
├── Employees
├── IT
├── Servers
├── Workstations
├── Groups

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

Employees  
IT  
Servers  
Workstations  
Groups  

---

# Part 2 — Create Users

## Step 3 — Employee Users

Navigate to:
Employees OU

Right-click → New → User

Create:

jdoe  
jsmith  
mjones  

Set password:
Cyberrange2026

Uncheck:
User must change password

Check:
Password never expires

---

## Step 4 — Admin User

Navigate to:
IT OU

Create:

itadmin

---

# Part 3 — Create Security Groups

## Step 5

Navigate to:
Groups OU

Create:

IT-Admins  
Employees  

---

## Step 6 — Assign Group Membership

### Add admin:

Open IT-Admins → Members → Add

Add:
itadmin

---

### Add employees:

Open Employees group

Add:
jdoe  
jsmith  
mjones  

---

# Part 4 — Organize Computers

## Step 7

Navigate to:
Computers container

Find:

WIN10-USER-01  
WIN11-USER-01  

Right-click → Move

Move to:
Workstations OU

---

# Part 5 — Verify Admin Access

## Step 8

Log into Windows 10 as:

CYBERRANGE\itadmin

---

## Step 9

Open Command Prompt (Admin)

Run:

whoami /groups

Verify:

IT-Admins  
Domain Admins  

---

# Part 6 — Create Group Policy

## Step 10

On Domain Controller:

Run:
gpmc.msc

---

## Step 11

Navigate to:

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

Navigate to:

Computer Configuration  
→ Policies  
→ Windows Settings  
→ Security Settings  
→ Advanced Audit Policy Configuration  
→ Audit Policies  

---

## Step 13 — Enable the following

Account Logon:
Credential Validation → Success, Failure

Account Management:
User Account Management → Success, Failure  
Security Group Management → Success, Failure  

Logon/Logoff:
Logon → Success, Failure  
Logoff → Success  

Privilege Use:
Sensitive Privilege Use → Success, Failure  

System:
System Integrity → Success, Failure  

---

# Part 8 — Enable Remote Desktop

Navigate to:

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

## Step 14 — Windows 10

Open Command Prompt as Administrator

Run:

gpupdate /force

Restart machine

---

## Step 15 — Windows 11

Run:

gpupdate /force

Restart machine

---

# Part 10 — Verify GPO Application

## Step 16

On Windows 10:

Open Command Prompt (Admin)

Run:

gpresult /r

---

## Step 17 — Verify Output

Under COMPUTER SETTINGS confirm:

Workstation-Baseline-GPO  
Default Domain Policy  

---

# Part 11 — Validate Logging

## Step 18

Generate activity:

- Log out
- Attempt incorrect login
- Log in successfully

---

## Step 19

Open:

Event Viewer  
→ Windows Logs  
→ Security  

---

## Step 20 — Verify Events

Look for:

4624 — Successful logon  
4634 — Logoff  
4672 — Special privileges  
5379 — Credential activity  

---

# Expected Results

- AD structure fully organized
- Users and groups created and assigned
- Workstations properly placed in OU
- GPO successfully applied
- GPO visible in gpresult
- Audit logs actively generated
- Domain environment behaves like enterprise network

---

# Key Concepts

- OUs provide structure and policy targeting
- Groups control access and permissions
- GPO enforces centralized configuration
- gpresult verifies policy application
- Event Viewer confirms real system behavior

---

# Common Mistakes

- Not running gpresult as admin
- Not linking GPO to correct OU
- Forgetting to restart machines
- Misplacing users or computers
- Assuming GPO works without verification

---

# Phase Completion Criteria

Phase 03 is complete when:

- OUs are created and populated
- Users and groups are configured
- Machines are in correct OUs
- GPO is created and linked
- GPO appears in gpresult
- Security logs are generated

---

# Summary

Phase 03 establishes centralized identity, structure, and policy enforcement across the cyber range. This phase marks the transition from a simple domain to a fully managed enterprise environment, enabling future attack simulations and SOC monitoring capabilities.
