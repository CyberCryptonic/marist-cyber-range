## Status

🚧 Functionally Complete

- File server deployed
- Shares created
- Permissions implemented
- Access control working

⚠️ May be extended later with additional enterprise services

# Phase 04 Lab Guide: Enterprise File Services Build

## Marist SOC Cyber Range

### Phase Overview
Phase 04 focused on expanding the target environment beyond basic Active Directory and Group Policy by adding a realistic enterprise file services server and configuring it so it behaves like a real company resource.

This phase documents the work completed for the **File Server / Enterprise File Services** portion of the range.

> **Important scope note:** Based on the work completed so far, the File Server portion of Phase 04 is complete. If your team defines Phase 04 as also including a Web Server (`WEB01`) or additional enterprise services, that portion would still remain for a later build. This guide documents the completed work that was actually performed.

---

## Phase 04 Objectives

The goal of this phase was to:

- Deploy a dedicated Windows Server 2022 file server
- Connect it to the target network
- Join it to the domain
- Create realistic enterprise shared folders
- Populate those folders with believable business data
- Create department users and security groups in Active Directory
- Apply role-based access control using NTFS permissions
- Create student accounts for later classroom use
- Validate that access changes based on the identity of the logged-in user

---

## Final Outcome

By the end of this phase, the environment included:

- A domain-joined **File-Server**
- Static network configuration on the target subnet
- Shared business folders
- Simulated enterprise data
- Department-based AD users
- Department-based security groups
- Student accounts for range use
- Group-based folder permissions
- A realistic enterprise file-share structure that can later support attack and detection scenarios

---

# 1. Build and Prepare the File Server

## 1.1 Create the VM
Create a new Windows Server 2022 VM in Proxmox.

Suggested role/name:

```text
File-Server
```

### Key requirements
- Use the target network
- Ensure the VM has a network adapter attached
- Ensure VirtIO drivers are installed if needed
- Confirm the server can communicate on the internal network

---

## 1.2 Fix missing network adapter / driver issues
If the server is missing network connectivity:

1. Open the VM hardware settings in Proxmox
2. Confirm a network adapter exists
3. Add a network adapter if one is missing
4. Boot the server
5. Install required VirtIO drivers if the NIC is not recognized
6. Reboot if necessary

---

## 1.3 Configure static IP addressing
On the File Server:

1. Open **Network Connections**
2. Open the properties of the Ethernet adapter
3. Open **Internet Protocol Version 4 (TCP/IPv4)**

Configure the server with a static address on the target subnet.

Example used in the environment:

```text
IP Address: 10.20.20.30
Subnet Mask: 255.255.255.0
Default Gateway: <target gateway>
Preferred DNS: <domain controller IP>
```

### Important
DNS should point to the **Domain Controller**, not to an external DNS server.

---

## 1.4 Verify connectivity
After setting the static IP:

1. Open Command Prompt
2. Test connectivity to the Domain Controller
3. Test connectivity to other target machines if available

Example:

```powershell
ping 10.20.20.10
```

---

# 2. Join the File Server to the Domain

## 2.1 Rename the server
Rename the machine to:

```text
File-Server
```

Then reboot.

---

## 2.2 Join the domain
On the File Server:

1. Open **Server Manager**
2. Click **Local Server**
3. Click the current **Workgroup** value
4. In **System Properties**, click **Change**
5. Select **Domain**
6. Enter your domain name

Example:

```text
cyberrange.local
```

7. Click **OK**
8. Enter domain admin credentials when prompted
9. Reboot the server

---

## 2.3 Verify domain join
After reboot:

1. Sign in with a domain account
2. Confirm the server appears in Active Directory
3. Confirm name resolution and login function properly

---

# 3. Create the Enterprise File Share Structure

## 3.1 Create the root share location
On the File Server, create:

```text
C:\Shares
```

> In this environment, the file server used the `C:` drive rather than `D:`. That is completely fine.

---

## 3.2 Create department folders
Inside `C:\Shares`, create the following folders:

```text
C:\Shares\
├── HR
├── Payroll
├── IT
├── Finance
├── Engineering
├── Legal
├── Executive
└── Public
```

---

# 4. Populate the File Server with Realistic Data

All files were created as `.txt` files because Office applications were not installed on the server. That is acceptable for this lab.

## 4.1 HR folder files
Create these files inside `C:\Shares\HR`:

```text
Employee-List.txt
Employee-Records.txt
Salary-Data.txt
Termination-Notes.txt
Writeups.txt
```

### Employee-List.txt
```text
Employee ID | Name | Department | Status
1001 | John Smith | IT | Active
1002 | Sarah Johnson | HR | Active
1003 | Michael Brown | Finance | Active
1004 | Emily Davis | Engineering | Active
1005 | Mark Wilson | IT | Terminated
```

### Employee-Records.txt
```text
Employee ID: 1002
Name: Sarah Johnson
Position: HR Specialist
Hire Date: 03/14/2021
Manager: HR Director
Status: Active
```

### Salary-Data.txt
```text
CONFIDENTIAL

John Smith - $85,000
Sarah Johnson - $78,000
Michael Brown - $92,000
Emily Davis - $88,000
```

### Termination-Notes.txt
```text
Employee: Mark Wilson
Employee ID: 1005
Department: IT
Termination Date: 02/14/2026
Reason: Violation of acceptable use policy
Handled By: HR Department
```

### Writeups.txt
```text
Employee: John Smith
Date: 01/10/2026
Issue: Repeated tardiness
Action: Written warning issued
Supervisor: IT Manager
```

---

## 4.2 Payroll folder files
Create these files inside `C:\Shares\Payroll`:

```text
Payroll-Q1.txt
Bonuses-2026.txt
```

### Payroll-Q1.txt
```text
Q1 Payroll Summary

John Smith - $21,250
Sarah Johnson - $19,500
Michael Brown - $23,000
Emily Davis - $22,000
```

### Bonuses-2026.txt
```text
Annual Bonus Distribution

John Smith - $5,000
Sarah Johnson - $4,500
Michael Brown - $6,000
Emily Davis - $5,500
```

---

## 4.3 IT folder files
Create these files inside `C:\Shares\IT`:

```text
Admin-Passwords.txt
Backup-Script.txt
Network-Config.txt
```

### Admin-Passwords.txt
```text
IT ADMIN CREDENTIALS

Domain Admin:
Username: administrator
Password: Winter2026!

Backup Service:
Username: backupsvc
Password: Backup123

Local Admin:
Username: admin
Password: Admin123
```

### Backup-Script.txt
```text
Backup Script Notes

Runs nightly at 02:00 AM
Backs up:
- File Server Shares
- Domain Controller

Destination:
\\File-Server\IT\Backups

Status: Active
```

### Network-Config.txt
```text
Network Configuration

Domain: cyberrange.local

File Server: 10.20.20.30
Domain Controller: 10.20.20.10

Subnets:
Red Team: 10.20.10.0/24
Target: 10.20.20.0/24
SOC: 10.20.30.0/24
```

---

## 4.4 Finance folder files
Create these files inside `C:\Shares\Finance`:

```text
Budget-2026.txt
Quarterly-Report.txt
```

### Budget-2026.txt
```text
2026 Annual Budget

IT Department: $500,000
HR Department: $250,000
Engineering: $750,000
Operations: $400,000

Total Budget: $1,900,000
```

### Quarterly-Report.txt
```text
Q1 Financial Report

Revenue: $2,500,000
Expenses: $1,800,000
Net Profit: $700,000

Notes:
- Increased spending in IT infrastructure
- Hiring expansion planned for Q2
```

---

## 4.5 Engineering folder files
Create these files inside `C:\Shares\Engineering`:

```text
Project-Alpha.txt
Design-Specs.txt
```

### Project-Alpha.txt
```text
Project Alpha Overview

Status: In Development
Lead: Emily Davis

Goals:
- Improve internal tooling
- Automate reporting systems
```

### Design-Specs.txt
```text
System Design Specifications

Architecture: 3-tier model
Frontend: Web-based UI
Backend: Internal API

Security:
- Authentication required
- Role-based access control
```

---

## 4.6 Legal folder files
Create these files inside `C:\Shares\Legal`:

```text
Contracts.txt
Compliance.txt
```

### Contracts.txt
```text
Client Contracts

Client: Central Hudson
Agreement: Cybersecurity Consulting
Start Date: 01/01/2026
End Date: 12/31/2026
```

### Compliance.txt
```text
Compliance Requirements

- HIPAA (if applicable)
- GDPR (data handling)
- Internal security policies

Audits performed annually
```

---

## 4.7 Executive folder files
Create these files inside `C:\Shares\Executive`:

```text
Acquisition-Plan.txt
Strategy-2026.txt
```

### Acquisition-Plan.txt
```text
Confidential Acquisition Plan

Target Company: SecureTech Inc.
Estimated Value: $3.5M

Goal:
Expand cybersecurity capabilities

Status: Under review
```

### Strategy-2026.txt
```text
Executive Strategy 2026

Goals:
- Expand cybersecurity services
- Increase client base by 20%
- Improve internal infrastructure

Focus Areas:
- Cloud security
- Threat detection
- Employee training
```

---

## 4.8 Public folder files
Create this file inside `C:\Shares\Public`:

```text
Company-Policy.txt
```

### Company-Policy.txt
```text
Company Acceptable Use Policy

- No unauthorized access
- No sharing credentials
- All activity may be monitored

Violations may result in termination
```

---

# 5. Create Users in Active Directory

This step was required before group-based permissions could be implemented.

## 5.1 Open Active Directory Users and Computers
On the Domain Controller:

1. Open **Server Manager**
2. Click **Tools**
3. Click **Active Directory Users and Computers**

---

## 5.2 Create or use department OUs
A clean AD structure was used, with departmental organization for users.

Example structure:

```text
Employees
├── HR
├── IT
├── Finance
└── Engineering
```

---

## 5.3 Create company users
Create a realistic set of users for the target environment.

Suggested usernames used in the environment:

```text
sjohnson   - HR
mwilson    - HR Manager
itadmin    - IT Admin
acarter    - IT
mbrown     - Finance
lwhite     - Finance
edavis     - Engineering
klee       - Engineering
```

### User creation process
For each user:

1. Right-click the correct OU
2. Click **New -> User**
3. Fill in:
   - First name
   - Last name
   - User logon name
4. Click **Next**
5. Set password
6. Uncheck **User must change password at next logon**
7. Check **Password never expires**
8. Finish creation

Example training password:

```text
Password123!
```

---

# 6. Create Student Accounts

Student accounts were created separately from company employee accounts.

This is important because:

- Company users represent the target organization
- Student users represent the people using the range in class

## 6.1 Create a Students OU
Example structure:

```text
Students
```

---

## 6.2 Create student accounts
Because the environment included six Windows client endpoints for users, six student accounts were created.

Example usernames:

```text
student01
student02
student03
student04
student05
student06
```

Use the same basic password standard if desired:

```text
Password123!
```

---

## 6.3 Create a STUDENTS security group
Create a group named:

```text
STUDENTS
```

Add all student accounts to that group.

---

# 7. Create Security Groups

Permissions were not assigned directly to users. Instead, the environment used **security groups**, which is the correct enterprise approach.

## 7.1 Create a Groups OU structure
Example clean structure:

```text
Groups
├── HR
├── IT
├── Finance
└── Engineering
```

---

## 7.2 Create these security groups
Create these groups as **Global** and **Security** groups:

```text
HR-Users
HR-Managers
IT-Users
IT-Admins
Finance-Users
Engineering-Users
STUDENTS
```

---

## 7.3 Add members to the groups

Example mappings:

### HR
```text
sjohnson  -> HR-Users
mwilson   -> HR-Managers
```

### IT
```text
itadmin   -> IT-Admins
acarter   -> IT-Users
```

### Finance
```text
mbrown    -> Finance-Users
lwhite    -> Finance-Users
```

### Engineering
```text
edavis    -> Engineering-Users
klee      -> Engineering-Users
```

### Students
```text
student01-student06 -> STUDENTS
```

> Important: users must exist before they can be added to groups.

---

# 8. Organize Active Directory Cleanly

The environment was reorganized so that users and groups were separated by function and by department.

## Recommended final layout

```text
cyberrange.local
├── Employees
│   ├── HR
│   ├── IT
│   ├── Finance
│   └── Engineering
├── Students
├── Groups
│   ├── HR
│   ├── IT
│   ├── Finance
│   └── Engineering
├── Servers
└── Workstations
```

## Why this matters
This creates a realistic enterprise layout where:

- OUs are used for organization and policy targeting
- Groups are used for access control
- Users are identities
- Machines are separate from users

---

# 9. Apply File Server Permissions

This is the core security portion of the phase.

## 9.1 Important Windows permissions concepts
Two rules were followed:

```text
Do not remove SYSTEM
Do not remove Administrators
```

Only broad user access was removed from sensitive folders.

---

## 9.2 Break inheritance on sensitive folders
Each department folder under `C:\Shares` inherited permissions from the parent directory.

To customize permissions:

1. Right-click the folder
2. Click **Properties**
3. Open the **Security** tab
4. Click **Advanced**
5. Click **Disable inheritance**
6. Choose:

```text
Convert inherited permissions into explicit permissions on this object
```

> Do not choose the option that removes all inherited permissions.

This was repeated for:

```text
HR
Payroll
IT
Finance
Engineering
Legal
Executive
```

`Public` was left more open by design.

---

## 9.3 Remove broad local user access
After inheritance was converted to explicit permissions, remove entries such as:

```text
Users (FILE-SERVER\Users)
```

from sensitive folders.

This prevents broad access and allows access to be controlled by AD groups instead.

---

## 9.4 Add group-based permissions

### HR
Add:

```text
HR-Users     -> Modify
HR-Managers  -> Full Control
```

### Payroll
Add:

```text
HR-Managers  -> Full Control
```

### IT
Add:

```text
IT-Users     -> Full Control
IT-Admins    -> Full Control
```

### Finance
Add:

```text
Finance-Users -> Modify
```

### Engineering
Add:

```text
Engineering-Users -> Modify
```

### Legal
Add:

```text
Domain Admins -> Full Control
```

### Executive
Add:

```text
Domain Admins -> Full Control
```

### Public
Keep broad access appropriate for collaboration, such as:

```text
Domain Users -> Modify
```

---

## 9.5 Keep administrative entries
The following entries were intentionally left in place where applicable:

```text
SYSTEM
Administrators
CREATOR OWNER
itadmin
```

`itadmin` was kept during build and administration to avoid accidental lockout and preserve management access.

---

## 9.6 Restrict IT-Admins where appropriate
At first, `IT-Admins` had broad access to every folder. That was later corrected to better reflect enterprise separation of duties.

Final model:

- `IT-Admins` remained on **IT**
- Optional on **Public**
- Removed from highly sensitive non-IT business folders such as:
  - HR
  - Payroll
  - Finance
  - Engineering
  - Legal
  - Executive

This better reflects real-world environments where IT manages systems but does not automatically have access to all departmental business data.

---

# 10. Validate Access

Permissions were tested from domain-joined Windows clients.

## 10.1 Test examples

### HR user
Log in as an HR user and test:

```text
\\File-Server\HR
```

Expected:
- access granted

Test:

```text
\\File-Server\IT
\\File-Server\Finance
```

Expected:
- access denied

---

### HR manager
Test:

```text
\\File-Server\HR
\\File-Server\Payroll
```

Expected:
- both allowed

---

### IT user
Test:

```text
\\File-Server\IT
```

Expected:
- allowed

Test:

```text
\\File-Server\HR
```

Expected:
- denied

---

### Finance user
Test:

```text
\\File-Server\Finance
```

Expected:
- allowed

Other department folders:
- denied

---

### Regular or student user
Test:

```text
\\File-Server\Public
```

Expected:
- allowed

Sensitive departments:
- denied

---

### Domain admin
Expected:
- access to all folders

---

# 11. Student and Endpoint Design Clarification

A key design decision during this phase was understanding that:

```text
Users are not the same thing as machines
```

The range included multiple Windows 10 and Windows 11 machines, but that did **not** mean each machine required one matching identity.

Instead:

- Users are identities
- Workstations are shared endpoints
- Multiple users can sign into the same machine
- Access is determined by group membership, not by the computer name

This matches real enterprise behavior and improves realism for later attack and defense scenarios.

---

# 12. Kali / Red Team Clarification

Another important design decision made during this phase:

- Kali systems do **not** need AD user accounts
- Kali systems should **not** be domain joined
- Kali systems **must** still be networked on the Red Team subnet
- Kali systems need connectivity to the target subnet so they can attack the environment

This means:

```text
Kali = attacker platform
AD users = identities inside the target environment
```

---

# 13. Troubleshooting Notes

## 13.1 Cannot paste into Proxmox console
The Proxmox console may not support normal clipboard behavior.

Workaround:
- Use RDP into Windows VMs when possible
- Then copy/paste file contents normally

---

## 13.2 Wrong object type in AD
A common mistake was creating OUs instead of groups.

Remember:

```text
OU = organization
Group = permissions
```

If a group shows a folder icon, it is an OU and should be replaced by a proper Security Group.

---

## 13.3 Protected from accidental deletion
If an OU cannot be deleted:

1. In ADUC, click **View -> Advanced Features**
2. Open the OU properties
3. Open the **Object** tab
4. Uncheck:

```text
Protect object from accidental deletion
```

Then delete it.

---

## 13.4 Cannot remove a permission entry
If Windows says a permission cannot be removed:

- it is likely inherited from the parent folder

Fix:
1. Open **Advanced Security Settings**
2. Click **Disable inheritance**
3. Choose:

```text
Convert inherited permissions into explicit permissions on this object
```

Then remove the unwanted entry.

---

# 14. Phase 04 Completion Summary

## What was completed
- File Server VM deployment
- Network configuration
- Domain join
- Share structure creation
- Realistic business data population
- AD company users
- AD student users
- Department security groups
- Group membership assignments
- Clean OU/group organization
- NTFS permission hardening
- Access testing

## What this enables next
This phase created the enterprise-side data and identity foundation required for:

- attack simulation
- insider threat scenarios
- file access auditing
- Security Onion visibility
- SOC detection content in Phase 05

---

