## Status

✅ Complete

- Organizational Units structured
- Department-based users created
- Student users created
- Security groups created and assigned
- Servers and workstations organized into OUs
- Group Policy deployed and verified
- Audit logging enabled
- Active Directory environment validated and operational

---

# Marist SOC Cyber Range
# Lab Build Guide — Phase 03: Active Directory Structure, Users, Groups, and Group Policy

---

# Purpose

This phase builds the core Active Directory structure for the target environment. The goal is to turn the domain into a realistic enterprise-style environment that supports centralized identity management, role-based access control, workstation organization, and baseline monitoring.

By the end of this phase, the environment will include:

- Department-based Organizational Units
- Employee and student user accounts
- Security groups for access control
- Organized server and workstation computer objects
- A baseline Group Policy Object
- Audit logging for authentication and account activity

This phase is important because it creates the identity and management foundation for everything that comes next, including file shares, server access, logging, attack simulation, and SOC monitoring.

---

# Objectives

- Create the Organizational Unit structure
- Create all employee and student users
- Create all required security groups
- Add users to the proper groups
- Organize computers into the proper OUs
- Create and link a workstation Group Policy Object
- Enable baseline audit logging
- Validate that the domain environment is functioning correctly

---

# Prerequisites

Before starting this phase, make sure the following are already completed:

- Proxmox environment is operational
- Primary Domain Controller is installed and working
- Domain has already been created as `cyberrange.local`
- DNS is functioning properly
- Windows 10 and Windows 11 client machines are joined to the domain
- You can log into the domain with an administrative account
- File Server has been joined to the domain if already built

---

# Environment Used

Domain Name:
`cyberrange.local`

Main Platform:
- Windows Server 2022 for the Domain Controller
- Windows 10 and Windows 11 for domain clients

Administrative Tools Used:
- Active Directory Users and Computers
- Group Policy Management
- Event Viewer
- Command Prompt
- PowerShell

---

# Target Active Directory Structure

The intended structure for this phase is:

cyberrange.local  
│  
├── Employees  
│   ├── Engineering  
│   ├── Finance  
│   ├── HR  
│   └── IT  
│  
├── STUDENTS  
│  
├── Groups  
│   ├── Engineering  
│   ├── Finance  
│   ├── HR  
│   ├── IT  
│   ├── STUDENTS  
│   └── IT-Admins  
│  
├── Servers  
└── Workstations  

This structure separates users, groups, servers, and workstations in a way that is easy to manage and easy to understand later when permissions, policies, and logging are expanded.

---

# Part 1 — Open Active Directory Users and Computers

## Step 1

Log into the Primary Domain Controller using a domain administrative account.

## Step 2

Open Active Directory Users and Computers.

You can do this either of these ways:

Method 1:
- Click Start
- Open Server Manager
- Go to Tools
- Click Active Directory Users and Computers

Method 2:
- Press `Windows + R`
- Type:
`dsa.msc`
- Press Enter

## Step 3

In the left panel, expand the domain:
`cyberrange.local`

You should now see the default domain containers and any OUs that already exist.

---

# Part 2 — Create the Organizational Unit Structure

## Step 4

Right-click `cyberrange.local`

Select:
- New
- Organizational Unit

## Step 5

Create the following top-level OUs one at a time:

- Employees
- STUDENTS
- Groups
- Servers
- Workstations

For each one:
- Type the name exactly
- Leave accidental deletion protection enabled unless you intentionally want it off
- Click OK

## Step 6

Now create the department OUs inside the `Employees` OU.

Right-click `Employees`

Select:
- New
- Organizational Unit

Create the following child OUs:

- Engineering
- Finance
- HR
- IT

When finished, your structure under `Employees` should contain all four departments.

## Step 7

Inside the `Groups` OU, create the departmental group containers if you want the exact visual structure you used.

Right-click `Groups`

Select:
- New
- Organizational Unit

Create:

- Engineering
- Finance
- HR
- IT
- STUDENTS

This gives you a clean place to store the actual security groups.

---

# Part 3 — Create Employee User Accounts

## Step 8

Navigate to:
`cyberrange.local > Employees > Engineering`

Right-click in the blank white area on the right side

Select:
- New
- User

## Step 9

Create the Engineering user.

Enter:
- First name: Emily
- Last name: Davis
- Full name: Emily Davis
- User logon name: choose the format you want to use consistently

Click Next

Set the password

Recommended lab configuration:
- Uncheck `User must change password at next logon`
- Check `Password never expires` if you want to keep the lab simple
- Make sure the account is enabled

Click Next, then Finish

## Step 10

Navigate to:
`cyberrange.local > Employees > Finance`

Create the Finance user:

- Michael Brown

Use the same process as above.

## Step 11

Navigate to:
`cyberrange.local > Employees > HR`

Create the HR user:

- Sarah Johnson

Use the same process as above.

## Step 12

Navigate to:
`cyberrange.local > Employees > IT`

Create the IT users:

- John Smith
- it admin

Use the same process for each account.

For `it admin`, make sure you remember the exact username format because this account will be used for administration and validation later.

---

# Part 4 — Create Student User Accounts

## Step 13

Navigate to:
`cyberrange.local > STUDENTS`

Right-click in the blank area

Select:
- New
- User

## Step 14

Create the following student accounts one at a time:

- Student 01
- Student 02
- Student 03
- Student 04
- Student 05
- Student 06

For each student:
- Set a password
- Uncheck `User must change password at next logon`
- Check `Password never expires` if you want to simplify the lab
- Ensure the account is enabled

When complete, all student accounts should appear inside the `STUDENTS` OU.

---

# Part 5 — Create Security Groups

## Step 15

Navigate to:
`cyberrange.local > Groups > Engineering`

Right-click in the blank white area

Select:
- New
- Group

## Step 16

Create the Engineering security group.

Use:
- Group name: Engineering
- Group scope: Global
- Group type: Security

Click OK

## Step 17

Navigate to:
`cyberrange.local > Groups > Finance`

Create:
- Finance

Set:
- Group scope: Global
- Group type: Security

## Step 18

Navigate to:
`cyberrange.local > Groups > HR`

Create:
- HR

If you also created manager groups in HR, you can create them here too, but for the baseline documented phase, the main HR group is enough unless you want to document both.

## Step 19

Navigate to:
`cyberrange.local > Groups > IT`

Create:
- IT
- IT-Admins

Set both as:
- Group scope: Global
- Group type: Security

## Step 20

Navigate to:
`cyberrange.local > Groups > STUDENTS`

Create:
- STUDENTS

Set:
- Group scope: Global
- Group type: Security

When done, all core security groups should exist.

---

# Part 6 — Add Users to the Correct Groups

This step is important because the users themselves should not be used directly for most permissions. Group membership is what makes the environment manageable.

## Step 21

Add the Engineering employee to the Engineering group.

Navigate to:
`cyberrange.local > Groups > Engineering`

Double-click the `Engineering` group

Go to:
- Members
- Add

Type the Engineering user account:
`Emily Davis`

Click:
- Check Names
- OK
- Apply
- OK

## Step 22

Add the Finance employee to the Finance group.

Open the `Finance` group

Add:
`Michael Brown`

Apply the changes

## Step 23

Add the HR employee to the HR group.

Open the `HR` group

Add:
`Sarah Johnson`

Apply the changes

## Step 24

Add the IT employee accounts to the correct IT groups.

Open the `IT` group

Add:
- John Smith

Then open the `IT-Admins` group

Add:
- it admin

If you want `it admin` to also be a normal IT member, you can add it there too, but at minimum it should be in `IT-Admins`.

## Step 25

Add all student accounts to the `STUDENTS` group.

Open the `STUDENTS` group

Go to:
- Members
- Add

Add:
- Student 01
- Student 02
- Student 03
- Student 04
- Student 05
- Student 06

Apply and close

## Step 26

Validate the memberships.

Open each group and confirm the correct users appear in the Members tab.

You should now have:

- Engineering group contains the Engineering employee
- Finance group contains the Finance employee
- HR group contains the HR employee
- IT group contains the IT employee
- IT-Admins contains the admin account
- STUDENTS contains all student accounts

---

# Part 7 — Organize Domain Computers

By default, newly joined computers often appear in the default `Computers` container. Moving them into the correct OUs makes policy application and management much easier.

## Step 27

In Active Directory Users and Computers, click the default `Computers` container.

Look for domain-joined systems such as:

- Windows 10 clients
- Windows 11 clients
- File Server if it has not already been moved

## Step 28

Move workstations into the Workstations OU.

For each client machine:
- Right-click the computer object
- Select Move
- Choose `Workstations`
- Click OK

Move all Windows 10 and Windows 11 systems into the `Workstations` OU.

## Step 29

Move server systems into the Servers OU.

For each server that should be there:
- Right-click the computer object
- Select Move
- Choose `Servers`
- Click OK

At minimum, the File Server should be in `Servers` if domain joined and visible there.

Do not move the Domain Controller into `Servers`. Domain Controllers remain in the default `Domain Controllers` OU unless you have a specific design reason to do otherwise.

## Step 30

Verify final placement.

After moving everything, confirm:
- All client workstations appear under `Workstations`
- File Server appears under `Servers`
- Domain Controller remains in `Domain Controllers`

---

# Part 8 — Create the Workstation Group Policy Object

This GPO establishes your workstation baseline and gives you centralized management.

## Step 31

Open Group Policy Management.

You can do this either way:

Method 1:
- Server Manager
- Tools
- Group Policy Management

Method 2:
- Press `Windows + R`
- Type:
`gpmc.msc`
- Press Enter

## Step 32

In the left pane, expand:

- Forest
- Domains
- cyberrange.local

Locate the `Workstations` OU

## Step 33

Right-click the `Workstations` OU

Select:
- Create a GPO in this domain, and Link it here

Name the GPO:
`Workstation-Baseline-GPO`

Click OK

## Step 34

Right-click `Workstation-Baseline-GPO`

Select:
- Edit

This opens the Group Policy Management Editor.

---

# Part 9 — Configure Audit Policy in the GPO

## Step 35

Inside the GPO editor, navigate to:

Computer Configuration  
→ Policies  
→ Windows Settings  
→ Security Settings  
→ Advanced Audit Policy Configuration  
→ Audit Policies  

## Step 36

Configure the following categories.

### Account Logon

Open:
- Credential Validation

Enable:
- Configure the following audit events
- Success
- Failure

Click Apply and OK

## Step 37

### Account Management

Open:
- User Account Management

Enable:
- Success
- Failure

Apply and OK

Then open:
- Security Group Management

Enable:
- Success
- Failure

Apply and OK

## Step 38

### Logon/Logoff

Open:
- Logon

Enable:
- Success
- Failure

Apply and OK

Then open:
- Logoff

Enable:
- Success

Apply and OK

## Step 39

### Privilege Use

Open:
- Sensitive Privilege Use

Enable:
- Success
- Failure

Apply and OK

## Step 40

### System

Open:
- System Integrity

Enable:
- Success
- Failure

Apply and OK

These settings provide useful log visibility for authentication, account use, group changes, and privilege activity.

---

# Part 10 — Enable Remote Desktop Through Group Policy

This allows easier administration and testing of workstations later in the build.

## Step 41

Still inside the GPO editor, navigate to:

Computer Configuration  
→ Policies  
→ Administrative Templates  
→ Windows Components  
→ Remote Desktop Services  
→ Remote Desktop Session Host  
→ Connections  

## Step 42

Open:
`Allow users to connect remotely using Remote Desktop Services`

Set it to:
- Enabled

Click Apply and OK

If you are using additional firewall rules or security settings later, document those separately, but enabling this policy establishes the workstation-side configuration.

---

# Part 11 — Apply Group Policy on the Client Machines

## Step 43

Log into each Windows 10 and Windows 11 workstation using an account with administrative privileges.

## Step 44

Open Command Prompt as Administrator.

Run:
`gpupdate /force`

Wait for the process to complete.

If prompted to log off or restart, do so.

## Step 45

Repeat this on all domain-joined workstation clients so they all receive the latest policy settings.

---

# Part 12 — Verify Group Policy Application

## Step 46

On a workstation, open Command Prompt as Administrator.

Run:
`gpresult /r`

## Step 47

Review the output carefully.

Under `COMPUTER SETTINGS`, confirm that the following appear:

- Workstation-Baseline-GPO
- Default Domain Policy

If `Workstation-Baseline-GPO` does not appear:
- Confirm the computer object is in the `Workstations` OU
- Confirm the GPO is linked to the `Workstations` OU
- Run `gpupdate /force` again
- Restart the machine and test again

## Step 48

Optionally, test on multiple workstations to confirm consistency across the environment.

---

# Part 13 — Validate Domain Authentication and Group Structure

## Step 49

Log into one or more workstations using different types of accounts:

- A student account
- A department employee account
- The IT admin account if needed for validation

Confirm that login succeeds and the domain is being used.

## Step 50

Open Command Prompt and run:
`whoami`

Verify the format is:
`cyberrange\username`

and not the local machine name.

## Step 51

If needed, check effective group membership by running:
`whoami /groups`

Confirm that the expected security groups appear for the logged-in user.

---

# Part 14 — Validate Audit Logging

## Step 52

Generate some test activity on a workstation:

- Log off
- Attempt one failed login
- Log in successfully
- If using the admin account, perform an elevated action

## Step 53

Open Event Viewer.

Navigate to:
Event Viewer  
→ Windows Logs  
→ Security  

## Step 54

Look for relevant security events such as:

- 4624 — Successful logon
- 4625 — Failed logon
- 4634 — Logoff
- 4672 — Special privileges assigned to new logon
- 4728 or related group membership events if group changes were made

The exact list may vary depending on what actions you performed, but you should clearly see authentication and security activity being recorded.

---

# Part 15 — Final Validation Checklist

Use this checklist to confirm Phase 03 is fully complete.

## Step 55

Confirm OU structure exists exactly as intended:

- Employees
- Employees\Engineering
- Employees\Finance
- Employees\HR
- Employees\IT
- STUDENTS
- Groups
- Groups\Engineering
- Groups\Finance
- Groups\HR
- Groups\IT
- Groups\STUDENTS
- Servers
- Workstations

## Step 56

Confirm all users exist:

Employees:
- Emily Davis
- Michael Brown
- Sarah Johnson
- John Smith
- it admin

Students:
- Student 01
- Student 02
- Student 03
- Student 04
- Student 05
- Student 06

## Step 57

Confirm all groups exist:

- Engineering
- Finance
- HR
- IT
- IT-Admins
- STUDENTS

## Step 58

Confirm group membership is correct:

- Emily Davis in Engineering
- Michael Brown in Finance
- Sarah Johnson in HR
- John Smith in IT
- it admin in IT-Admins
- Student 01 through Student 06 in STUDENTS

## Step 59

Confirm computer placement is correct:

- All Windows 10 and Windows 11 clients in Workstations
- File Server in Servers
- Domain Controller remains in Domain Controllers

## Step 60

Confirm policy and logging work:

- `gpresult /r` shows Workstation-Baseline-GPO
- Security logs show authentication events
- Domain login works across clients

---

# Expected Results

When this phase is fully complete, the environment should behave like a centrally managed domain.

You should have:

- A clean Active Directory OU structure
- Clearly organized users and groups
- Proper user-to-group assignments
- Workstations separated from servers
- A functioning workstation baseline GPO
- Security logging that can later support SOC analysis
- A domain environment that is easier to manage, scale, and monitor

---

# Common Mistakes to Avoid

- Creating users in the wrong OU
- Forgetting to add users to groups
- Leaving workstation computer objects in the default Computers container
- Moving the Domain Controller out of the Domain Controllers OU
- Linking the GPO to the wrong OU
- Running `gpresult /r` before forcing policy updates
- Assuming audit policy works without checking Event Viewer
- Using inconsistent naming for users or groups

---

# Why This Phase Matters

This phase is the identity and management backbone of the cyber range.

Without this structure:

- Permissions become messy
- Workstations are harder to manage
- Logging is inconsistent
- Later file server and attack simulation steps become much harder

With this structure in place:

- Users can be managed centrally
- Access can be controlled using groups
- Systems can receive policies based on OU placement
- Authentication and privilege activity can be tracked
- The lab starts to behave like a realistic enterprise environment

---

# Phase Completion Criteria

Phase 03 is complete when all of the following are true:

- The OU structure is built
- All users are created
- All security groups are created
- All users are added to the proper groups
- Workstations and servers are placed in their correct OUs
- The workstation GPO is linked and applied
- Audit logs are being generated and verified
- Domain authentication works correctly across the target environment

---

# Transition to the Next Phase

After this phase, the next major build activities include:

- File server deployment and shared folder permissions
- Additional target environment server builds
- Web server deployment
- Vulnerable application deployment
- Centralized logging expansion
- SOC telemetry integration

This phase is the point where the cyber range stops being a collection of machines and becomes a manageable enterprise-style lab.

---

# Summary

Phase 03 established the Active Directory structure for the target environment inside `cyberrange.local`.

The build included:
- Department-based Organizational Units
- Employee and student user accounts
- Security groups for access control
- User-to-group assignment
- Server and workstation organization
- A workstation baseline Group Policy Object
- Audit logging for authentication and account activity

At the end of this phase, the environment is organized, centrally managed, and ready for continued expansion into file services, target infrastructure, attack simulation, and SOC visibility.
