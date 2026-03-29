## Status

✅ Completed

- Users created  
- Groups implemented  
- Group memberships assigned  
- Workstations organized into the correct OU  
- GPO deployed  
- Audit logging enabled  
- Policy application verified  
- Logging validated  
- Administrative access confirmed  

---

# Marist SOC Cyber Range  
# Lab Build Guide — Phase 03: Active Directory Structure, Users, Groups, and Group Policy

Source File: :contentReference[oaicite:0]{index=0}

---

# Purpose

Phase 03 transforms the cyber range from a basic Active Directory deployment into a structured, enterprise-managed environment.

This phase introduces:

- Organizational structure through Organizational Units (OUs)  
- Identity management through user creation  
- Role-based access control through security groups  
- Centralized configuration through Group Policy  
- Security visibility through audit logging  

By the end of this phase, the environment behaves like a real enterprise network and is prepared for later expansion into file services, access control, and SOC monitoring.

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

Before beginning this phase, the following must already be complete:

- Proxmox environment is operational  
- Domain Controller is installed and functioning  
- Domain `cyberrange.local` exists  
- Windows 10 and Windows 11 systems are joined to the domain  
- Domain authentication is functioning properly  

---

# Target Active Directory Structure

The target structure used in this phase is:

cyberrange.local  
│  
├── Employees  
├── IT  
├── Servers  
├── Workstations  
├── Groups  

This structure is used to separate users, administrative accounts, computer objects, and security groups so the environment can be managed more like a real enterprise network.

---

# Part 1 — Create Organizational Units (OUs)

## Step 1 — Log into the Domain Controller

Log into the Domain Controller using an account with domain administrative privileges.

This phase was performed from the Domain Controller because Active Directory management and Group Policy configuration were handled centrally from that system.

---

## Step 2 — Open Active Directory Users and Computers

Open:

Active Directory Users and Computers  

Expand:

cyberrange.local  

This is the primary tool used to create the OU structure, user objects, group objects, and to move computer objects into the correct locations.

---

## Step 3 — Create Top-Level Organizational Units

Right-click the domain:

New → Organizational Unit  

Create the following OUs:

- Employees  
- IT  
- Servers  
- Workstations  
- Groups  

These OUs establish the initial enterprise structure for the cyber range.

Purpose of each OU:

- Employees → stores standard employee user accounts  
- IT → stores administrative or IT-related accounts  
- Servers → intended location for server computer objects  
- Workstations → intended location for Windows client computer objects  
- Groups → stores security groups used for access control and management  

At the end of this step, the domain should no longer rely only on the default Users and Computers containers.

---

# Part 2 — Create User Accounts

## Step 4 — Create Standard Employee Users

Navigate to:

Employees OU  

Right-click:

New → User  

Create the following employee user accounts:

- jdoe  
- jsmith  
- mjones  

For each user, set the password to:

Cyberrange2026  

Configure each user account with the following settings:

- Disable `User must change password at next logon`  
- Enable `Password never expires`  

This was done to keep the lab environment simple and consistent so future testing and demonstrations are not interrupted by forced password changes or expiration issues.

---

## Step 5 — Create the Administrative User

Navigate to:

IT OU  

Right-click:

New → User  

Create the following administrative account:

- itadmin  

This account is used later in the phase to validate administrative access, domain authentication, and group membership.

---

# Part 3 — Create Security Groups

## Step 6 — Create the Initial Security Groups

Navigate to:

Groups OU  

Right-click:

New → Group  

Create the following groups:

- IT-Admins  
- Employees  

These groups establish the first layer of role-based access control within the environment.

Purpose of each group:

- IT-Admins → administrative group for elevated access  
- Employees → standard group for normal employee accounts  

---

## Step 7 — Assign Group Memberships

Open the `IT-Admins` group.

Add:

- itadmin  

Then open the `Employees` group.

Add:

- jdoe  
- jsmith  
- mjones  

This step is important because user permissions and administrative roles should be tied to group membership rather than handled user-by-user whenever possible.

At the end of this step:

- `itadmin` is in `IT-Admins`  
- `jdoe`, `jsmith`, and `mjones` are in `Employees`  

---

# Part 4 — Organize Domain Computers

## Step 8 — Open the Default Computers Container

In Active Directory Users and Computers, navigate to:

Computers container  

Locate all domain-joined Windows client systems.

The systems identified in this phase were:

- Windows 10 machines  
- Windows 11 machines  

By default, newly joined machines often appear in the generic Computers container. This is functional, but not ideal for organization or Group Policy targeting.

---

## Step 9 — Move Workstations into the Workstations OU

For each domain-joined Windows 10 and Windows 11 machine:

- Right-click the computer object  
- Select Move  
- Choose the Workstations OU  
- Click OK  

This step ensures that workstation systems are organized properly and can later receive policies scoped specifically to workstation systems.

At the end of this step, the Windows client systems should no longer be left inside the default Computers container.

---

# Part 5 — Verify Administrative Access

## Step 10 — Log Into a Workstation as itadmin

Log into a domain-joined workstation using:

CYBERRANGE\itadmin  

This test confirms that the account exists, the domain authentication process is working, and the workstation can successfully authenticate the administrative account through Active Directory.

---

## Step 11 — Verify Group Membership from the Workstation

Open Command Prompt as Administrator.

Run:

whoami /groups  

Review the output and confirm that it includes:

- IT-Admins  
- Domain Admins  

This step verifies that the administrative account is receiving the expected group memberships and is functioning with elevated access as intended.

---

# Part 6 — Create and Link a Group Policy Object

## Step 12 — Open Group Policy Management

On the Domain Controller, open Group Policy Management by running:

gpmc.msc  

This tool is used to create, link, and edit Group Policy Objects within the domain.

---

## Step 13 — Create a Workstation Baseline GPO

In Group Policy Management, navigate to:

cyberrange.local → Workstations OU  

Right-click the Workstations OU and select:

Create a GPO in this domain, and link it here  

Name the GPO:

Workstation-Baseline-GPO  

This GPO is linked directly to the Workstations OU so that the workstation systems moved there in the earlier step will receive the policy.

---

## Step 14 — Edit the New GPO

Right-click:

Workstation-Baseline-GPO  

Select:

Edit  

This opens the Group Policy editor so audit policy and Remote Desktop settings can be configured.

---

# Part 7 — Configure Audit Policy

## Step 15 — Navigate to Advanced Audit Policy Configuration

Inside the GPO editor, navigate to:

Computer Configuration  
→ Policies  
→ Windows Settings  
→ Security Settings  
→ Advanced Audit Policy Configuration  
→ Audit Policies  

This section is used to configure the security events that Windows systems will record.

---

## Step 16 — Enable the Required Audit Categories

Enable the following logging settings:

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

These settings were selected to provide baseline security visibility into authentication activity, group and user changes, privileged actions, and system integrity events.

At the end of this step, the GPO contains the audit policy needed for later verification and future SOC use.

---

# Part 8 — Enable Remote Desktop Through Group Policy

## Step 17 — Navigate to the Remote Desktop Policy

Still inside the GPO editor, navigate to:

Computer Configuration  
→ Administrative Templates  
→ Windows Components  
→ Remote Desktop Services  
→ Remote Desktop Session Host  
→ Connections  

This path contains the policy used to allow Remote Desktop connections to workstation systems.

---

## Step 18 — Enable the Policy

Open:

Allow users to connect remotely using Remote Desktop Services  

Set the policy to:

Enabled  

This step allows workstation systems receiving the GPO to accept Remote Desktop connections, which supports administration and later lab activity.

---

# Part 9 — Apply Group Policy on Workstations

## Step 19 — Update Policy on All Workstations

On all workstation systems, open Command Prompt as Administrator.

Run:

gpupdate /force  

After the update completes, restart the workstation.

This step is necessary to ensure the new policy settings are applied immediately rather than waiting for normal background refresh timing.

---

# Part 10 — Verify GPO Application

## Step 20 — Run gpresult on a Workstation

On a workstation, open Command Prompt as Administrator.

Run:

gpresult /r  

This command displays which Group Policy Objects are being applied to the system.

---

## Step 21 — Confirm the Correct Policies Are Applied

Under `COMPUTER SETTINGS`, confirm the output includes:

- Workstation-Baseline-GPO  
- Default Domain Policy  

This verifies that:

- the GPO is linked correctly  
- the workstation is in the correct OU  
- the policy was successfully applied  

At this point, policy enforcement for the workstation baseline has been validated.

---

# Part 11 — Validate Audit Logging

## Step 22 — Generate Test Activity

On a workstation, generate normal authentication activity by doing the following:

- Log out  
- Attempt a failed login  
- Log in successfully  

These actions are used to generate security events that should be captured by the audit policy configured earlier.

---

## Step 23 — Open Event Viewer

Open:

Event Viewer  
→ Windows Logs  
→ Security  

This log is where authentication and security events generated by the configured policy will appear.

---

## Step 24 — Verify Expected Security Events

Confirm that the following events are present:

- 4624 — Successful logon  
- 4634 — Logoff  
- 4672 — Privileged logon  
- 5379 — Credential activity  

This step proves that audit logging is not just configured, but actively working on the workstation systems.

---

# Expected Results

By the end of Phase 03, the following results should be true:

- The Active Directory structure is organized using OUs  
- User accounts have been created  
- Security groups have been created  
- Group memberships have been assigned  
- Workstations have been placed in the correct OU  
- Group Policy has been linked and applied successfully  
- Audit logging is active  
- Security events are visible in Event Viewer  
- Administrative access has been confirmed  

---

# Key Concepts

- OUs define structure and scope for administration and policy  
- Groups provide role-based access control  
- Group Policy provides centralized configuration  
- `gpresult` is used to verify policy application  
- Event Viewer is used to validate audit logging and security visibility  

---

# Common Mistakes

- Not linking the GPO to the correct OU  
- Not restarting systems after `gpupdate /force`  
- Leaving workstation computer objects in the wrong container  
- Running `gpresult /r` without administrative privileges  
- Assuming audit policy is working without checking Event Viewer  

---

# Current Environment State

At the end of this phase:

- Users and groups are implemented  
- Group memberships are assigned  
- Workstations are organized into the proper OU  
- The workstation baseline GPO is deployed and functioning  
- Audit logging is enabled and validated  
- The domain environment is operational and managed more like an enterprise network  

Because validation was completed, this phase should now be considered complete.

---

# Phase Completion Criteria

Phase 03 is complete when all of the following are true:

- OUs are structured  
- Users and groups are created  
- Group memberships are assigned correctly  
- Workstations are placed in the correct OU  
- The GPO is created, linked, and applied  
- The GPO appears in `gpresult`  
- Security logs are consistently generated  
- Administrative access is verified  

---

# Transition to Phase 04

The next phase focuses on:

- File server deployment  
- Shared folder structure  
- Access control using AD groups  
- Permission enforcement  

---

# Summary

Phase 03 establishes centralized identity organization, access control, Group Policy enforcement, and audit visibility across the cyber range.

This phase moves the environment from a simple domain deployment into a structured, managed enterprise system, providing the control and visibility needed for later enterprise services and security operations.
