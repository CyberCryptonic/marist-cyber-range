## Status

✅ Completed

- File Server deployed  
- Shares created  
- Permissions implemented  
- Access control validated  
- Enterprise-style data populated  
- File services functioning properly  

---

# Marist SOC Cyber Range  
# Lab Build Guide — Phase 04: Enterprise File Services

Source File: :contentReference[oaicite:0]{index=0}

---

# Purpose

Phase 04 expands the cyber range from identity and policy management into a real enterprise data environment.

This phase introduces:

- Centralized file storage  
- Department-based data separation  
- Role-based access control using Active Directory groups  
- Realistic business data for attack and detection scenarios  

By the end of this phase, the environment behaves more like a real company network where data access depends on identity. This is important because it gives both the Red Team and the SOC meaningful resources to attack, defend, and monitor.

---

# Objectives

- Deploy a domain-joined File Server  
- Configure static networking  
- Create enterprise-style shared folders  
- Populate folders with realistic data  
- Create department users and groups  
- Apply NTFS permissions using groups  
- Validate access control behavior  

---

# Prerequisites

Before beginning this phase, the following must already be complete:

- Domain Controller is operational  
- Active Directory is configured  
- Users and groups already exist or are ready to be created  
- Windows 10 and Windows 11 endpoints are domain joined  
- The Target network is functioning on `10.20.20.0/24`  

---

# Final Outcome

By the end of this phase:

- The File Server is deployed and joined to the domain  
- Department shares exist  
- Data is populated in shared folders  
- Permissions are enforced using Active Directory groups  
- Access control is working as designed  

---

# Part 1 — Build the File Server

## Step 1 — Create the Virtual Machine

Create a new Windows Server 2022 VM.

Use the following configuration details:

- Name: `File-Server`  
- Network: Target subnet  
- Ensure the NIC is attached  

This VM will act as the central file storage server for the Target Environment.

---

## Step 2 — Fix Network Issues if Needed

If the VM boots but has no connectivity:

- Verify that the network adapter exists in Proxmox  
- Install VirtIO drivers if required  
- Reboot the system  

This ensures the server can communicate on the target network before any domain or file service configuration is attempted.

---

## Step 3 — Configure Static IPv4 Settings

Assign the following static IP settings to the server:

IP Address: `10.20.20.30`  
Subnet Mask: `255.255.255.0`  
Gateway: `10.20.20.1`  
DNS: `10.20.20.10`  
Secondary DNS: `10.20.20.11`

Important:

- DHCP is managed externally in this environment (not on domain controllers)
- All domain-joined systems must use the domain controllers for DNS
- Primary DNS: 10.20.20.10
- Secondary DNS: 10.20.20.11

This gives the File Server a fixed address and points it to the Domain Controller for DNS resolution.

---

## Step 4 — Verify Connectivity

Open Command Prompt and run:

`ping 10.20.20.10`

Successful replies confirm that the File Server can communicate with the Domain Controller.

---

# Part 2 — Join the File Server to the Domain

## Step 5 — Rename the Server

Rename the machine to:

`File-Server`

Reboot the server after renaming.

Using the intended hostname first helps keep the domain clean and avoids renaming the machine later after it has already joined Active Directory.

---

## Step 6 — Join the Domain

Open Server Manager and change the system from Workgroup membership to Domain membership.

Join the following domain:

`cyberrange.local`

When prompted, enter administrative credentials.

Reboot after the join completes.

---

## Step 7 — Validate the Domain Join

After reboot:

- Log in with a domain account  
- Confirm that the File Server appears in Active Directory  

This verifies that the domain join completed successfully and the server is now part of the enterprise environment.

---

# Part 3 — Create the Share Structure

## Step 8 — Create the Root Folder

Create the following folder on the C: drive:

`C:\Shares`

This folder will serve as the parent location for all departmental shares.

---

## Step 9 — Create Department Folders

Inside `C:\Shares`, create the following folders:

- HR  
- Payroll  
- IT  
- Finance  
- Engineering  
- Legal  
- Executive  
- Public  

The final folder structure should be:

`C:\Shares\HR`  
`C:\Shares\Payroll`  
`C:\Shares\IT`  
`C:\Shares\Finance`  
`C:\Shares\Engineering`  
`C:\Shares\Legal`  
`C:\Shares\Executive`  
`C:\Shares\Public`  

This structure simulates how a real company separates departmental data.

---

# Part 4 — Populate the File Shares with Data

## Step 10 — Create Example Business Files

Create `.txt` files inside the departmental folders to simulate real enterprise data.

Use the following examples:

### HR
- Employee-List.txt  
- Salary-Data.txt  
- Termination-Notes.txt  

### IT
- Admin-Passwords.txt  
- Network-Config.txt  

### Finance
- Budget-2026.txt  

### Executive
- Strategy-2026.txt  

### Public
- Company-Policy.txt  

These files provide realistic content for later use in access-control testing, attack simulation, and SOC monitoring scenarios.

---

# Part 5 — Create Active Directory Users

## Step 11 — Create Company Users

Create the following example users:

- `sjohnson` → HR  
- `mwilson` → HR Manager  
- `itadmin` → IT  
- `acarter` → IT  
- `mbrown` → Finance  
- `lwhite` → Finance  
- `edavis` → Engineering  
- `klee` → Engineering  

These users represent normal enterprise accounts that will be used to test permissions and access behavior.

---

## Step 12 — Create Student Users

Create the following student accounts:

- `student01`  
- `student02`  
- `student03`  
- `student04`  
- `student05`  
- `student06`  

These users provide additional accounts for access testing and training scenarios.

---

## Step 13 — Create the STUDENTS Group

Create:

`STUDENTS`

Add all student users to this group.

This allows permissions to be managed through a single group rather than assigning permissions account by account.

---

# Part 6 — Create Security Groups

## Step 14 — Create Department and Role Groups

Create the following security groups:

- `HR-Users`  
- `HR-Managers`  
- `IT-Users`  
- `IT-Admins`  
- `Finance-Users`  
- `Engineering-Users`  
- `STUDENTS`  

These groups are used to apply permissions to folders based on role and department.

---

## Step 15 — Assign Group Membership

Add users to the correct groups.

Examples given in this phase:

- `sjohnson` → `HR-Users`  
- `mwilson` → `HR-Managers`  
- `itadmin` → `IT-Admins`  

Follow the same pattern for the other department users.

This is a critical step because permissions in this phase are based on groups, not direct user assignments.

---

# Part 7 — Apply Folder Permissions

## Step 16 — Open Advanced Security Settings

For each sensitive folder:

- Right-click the folder  
- Select Properties  
- Open the Security tab  
- Click Advanced  

This is where the folder’s NTFS permissions are modified.

---

## Step 17 — Break Inheritance

For each sensitive folder:

- Click Disable inheritance  
- Choose Convert inherited permissions  

This preserves the existing entries as editable explicit permissions and allows custom access control to be applied to each folder.

---

## Step 18 — Remove Broad Access

Remove:

`Users (local)`

This is done so that broad or overly permissive local access is removed before the department-based permissions are applied.

---

## Step 19 — Apply Group-Based Permissions

Apply the following NTFS permissions to the folders.

### HR
- `HR-Users` → Modify  
- `HR-Managers` → Full Control  

### Payroll
- `HR-Managers` → Full Control  

### IT
- `IT-Users` → Full Control  
- `IT-Admins` → Full Control  

### Finance
- `Finance-Users` → Modify  

### Engineering
- `Engineering-Users` → Modify  

### Public
- `Domain Users` → Modify  

These permissions implement role-based access control using Active Directory groups.

---

## Step 20 — Keep Required Entries

Do not remove the following entries:

- `SYSTEM`  
- `Administrators`  
- `CREATOR OWNER`  

These are required system or administrative entries that should remain in place.

---

# Part 8 — Validate Access

## Step 21 — Test Access by Role

From a client machine, test file share access using different user accounts.

### HR User
Verify:

`\\File-Server\HR` → Allowed  
`\\File-Server\IT` → Denied  

### IT User
Verify:

`\\File-Server\IT` → Allowed  
`\\File-Server\HR` → Denied  

### Student
Verify:

`\\File-Server\Public` → Allowed  

This step confirms that folder access behaves according to group membership.

---

# Part 9 — Key Concepts

This phase is built on several core concepts:

- Access is based on groups, not users  
- Users are separate from machines  
- The File Server becomes the central enterprise data source  
- Permissions are used to enforce least privilege  

These concepts are what make the file services environment behave like a real enterprise network.

---

# Part 10 — Troubleshooting

## Issue — Cannot Remove a Permission Entry

Fix:

Disable inheritance first

If permissions are inherited, some entries cannot be removed until inheritance is disabled and converted.

---

## Issue — Wrong Active Directory Object Used

Important reminder:

`OU ≠ Group`

An Organizational Unit is used for structure and administration.

A Group is used for assigning permissions.

They are not interchangeable.

---

## Issue — Cannot Delete an OU

Fix:

Disable:

`Protect object from accidental deletion`

This is a common issue when trying to modify or remove Organizational Units.

---

# Phase Completion Summary

At the completion of this phase:

- File Server is deployed  
- Shares are created  
- Active Directory users and groups are created  
- Group-based permissions are implemented  
- Access validation is successful  

Because validation was completed and access control is functioning, this phase should now be considered complete.

---

# Current Environment State

At the end of this phase, the Target Environment is:

- Fully functional  
- Enterprise-like  
- Ready for attack simulation  
- Ready for SOC monitoring  

This means the environment now contains centralized data, controlled access, and realistic enterprise structure.

---

# Next Phase

Next phase:

Target Environment finalization.

---

# Summary

Phase 04 introduces real enterprise data and access control into the cyber range.

This phase transforms the environment from a structured network into a realistic organization by adding:

- Centralized file storage  
- Department-based separation of data  
- Group-based access control  
- Realistic business files for attack and monitoring scenarios  

With this phase complete, the environment is better prepared for insider threat scenarios, credential abuse, file access monitoring, and broader SOC detection use cases.
