## Status

🚧 Functionally Complete

- File server deployed  
- Shares created  
- Permissions implemented  
- Access control working  

⚠️ May be extended later with additional enterprise services  

---

# Marist SOC Cyber Range  
# Lab Build Guide — Phase 04: Enterprise File Services

---

# Purpose

Phase 04 expands the cyber range from identity and policy management into a **real enterprise data environment**.

This phase introduces:

- Centralized file storage  
- Department-based data separation  
- Role-based access control (RBAC) using AD groups  
- Realistic business data for attack and detection scenarios  

By completing this phase, the environment now behaves like a real company network where **data access depends on identity**, which is critical for both red team and SOC operations.

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

- Domain Controller operational  
- Active Directory configured (Phase 02 & 03 complete)  
- Users and groups created  
- Windows 10/11 endpoints domain joined  
- Target network functioning (10.20.20.0/24)  

---

# Final Outcome

By the end of this phase:

- File Server is deployed and domain joined  
- Department shares exist  
- Data is populated  
- Permissions are enforced using AD groups  
- Users see only what they are supposed to see  

---

# Part 1 — Build File Server

## Step 1 — Create VM

Create Windows Server 2022 VM:

- Name: `File-Server`  
- Network: Target subnet  
- Ensure NIC is attached  

---

## Step 2 — Fix Network (if needed)

If no connectivity:

- Verify network adapter exists in Proxmox  
- Install VirtIO drivers if required  
- Reboot  

---

## Step 3 — Configure Static IP

```
IP Address: 10.20.20.30  
Subnet Mask: 255.255.255.0  
Gateway: 10.20.20.1  
DNS: 10.20.20.10  
```

---

## Step 4 — Verify Connectivity

```
ping 10.20.20.10
```

---

# Part 2 — Join Domain

## Step 5 — Rename Server

```
File-Server
```

Reboot  

---

## Step 6 — Join Domain

- Open Server Manager  
- Change from Workgroup → Domain  

```
cyberrange.local
```

- Enter admin credentials  
- Reboot  

---

## Step 7 — Validate

- Login with domain account  
- Confirm server appears in AD  

---

# Part 3 — Create Share Structure

## Step 8 — Create Root Folder

```
C:\Shares
```

---

## Step 9 — Create Departments

```
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

# Part 4 — Populate Data

Create `.txt` files to simulate real enterprise data.

## Example Sensitive Data

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

---

# Part 5 — Active Directory Users

## Step 10 — Create Company Users

Example:

```
sjohnson   - HR  
mwilson    - HR Manager  
itadmin    - IT  
acarter    - IT  
mbrown     - Finance  
lwhite     - Finance  
edavis     - Engineering  
klee       - Engineering  
```

---

## Step 11 — Create Student Users

```
student01 → student06
```

---

## Step 12 — Create STUDENTS Group

Add all student users  

---

# Part 6 — Create Security Groups

## Step 13 — Create Groups

```
HR-Users  
HR-Managers  
IT-Users  
IT-Admins  
Finance-Users  
Engineering-Users  
STUDENTS  
```

---

## Step 14 — Assign Members

Example:

```
sjohnson → HR-Users  
mwilson → HR-Managers  
itadmin → IT-Admins  
```

---

# Part 7 — Apply Permissions

## Step 15 — Break Inheritance

For each sensitive folder:

- Properties → Security → Advanced  
- Disable inheritance  
- Convert permissions  

---

## Step 16 — Remove Broad Access

Remove:

```
Users (local)
```

---

## Step 17 — Apply Group-Based Permissions

### HR
```
HR-Users → Modify  
HR-Managers → Full Control  
```

### Payroll
```
HR-Managers → Full Control  
```

### IT
```
IT-Users → Full Control  
IT-Admins → Full Control  
```

### Finance
```
Finance-Users → Modify  
```

### Engineering
```
Engineering-Users → Modify  
```

### Public
```
Domain Users → Modify  
```

---

## Step 18 — Keep Required Entries

Do NOT remove:

```
SYSTEM  
Administrators  
CREATOR OWNER  
```

---

# Part 8 — Validate Access

## Step 19 — Test by Role

### HR User
```
\\File-Server\HR → Allowed  
\\File-Server\IT → Denied  
```

### IT User
```
\\File-Server\IT → Allowed  
\\File-Server\HR → Denied  
```

### Student
```
\\File-Server\Public → Allowed  
```

---

# Part 9 — Key Concepts

- Access is based on **groups**, not users  
- Users ≠ machines  
- File server is central data source  
- Permissions enforce least privilege  

---

# Part 10 — Troubleshooting

## Cannot remove permission
→ Disable inheritance first  

## Wrong AD object
```
OU ≠ Group
```

## Cannot delete OU
→ Disable "protect from accidental deletion"  

---

# Phase Completion Summary

## Completed

- File Server deployed  
- Shares created  
- AD users and groups created  
- Group-based permissions implemented  
- Access validation successful  

---

# Current Environment State

The Target Environment is now:

- Fully functional  
- Enterprise-like  
- Ready for attack simulation  
- Ready for SOC monitoring  

Remaining:

- Minor permission tuning  
- OU cleanup  
- Final validation  

---

# Next Phase

➡️ SOC / Detection Environment Setup  

---

# Summary

Phase 04 introduces real enterprise data and access control into the cyber range.

This transforms the environment from a structured network into a **realistic organization**, enabling:

- Insider threat scenarios  
- Credential abuse attacks  
- File access monitoring  
- SOC detection use cases  
