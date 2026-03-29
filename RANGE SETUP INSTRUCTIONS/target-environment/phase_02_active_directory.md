## Status

✅ Completed

# Marist SOC Cyber Range
# Lab Build Guide — Phase 02: Active Directory Deployment and Domain Setup

Source File: :contentReference[oaicite:0]{index=0}

---

# Purpose

This phase transitions the cyber range from a base Proxmox infrastructure into a functioning Windows enterprise domain environment.

This phase focuses on:

- Cloning Windows systems from Proxmox templates
- Completing Windows installation where required
- Installing VirtIO drivers
- Configuring the first server as the Domain Controller
- Installing Active Directory Domain Services (AD DS)
- Creating the `cyberrange.local` domain
- Configuring DNS
- Joining Windows endpoints to the domain
- Creating the initial Active Directory structure

By the end of this phase, the environment supports centralized authentication and begins functioning like a real enterprise network.

---

# Phase Objective

The goal of this phase is to establish the identity and authentication backbone of the cyber range.

Before this phase:
- Only infrastructure and networking existed

After this phase:
- Domain Controller is operational
- Active Directory is installed
- DNS is integrated
- Domain authentication works
- Windows endpoints are domain joined

---

# Systems Used in This Phase

## Templates Used

- `904 (Windows-10-EduN)`
- `905 (Windows-11-EduN)`
- `906 (Windows-Server-2022)`

## Initial Virtual Machines Built

All systems are placed on:
- Network: `vmbr2`
- Subnet: `10.20.20.0/24`

Systems:

- Primary-Domain-Server
- Windows10-User-01
- Windows11-User-01

---

# Part 1 — Clone Virtual Machines in Proxmox

## Step 1 — Clone Domain Controller

In Proxmox:

- Select template: `906 (Windows-Server-2022)`
- Clone VM
- Name it:

Primary-Domain-Server

- Attach to network:
vmbr2

Start the VM

---

## Step 2 — Clone Windows Clients

Repeat for:

Windows 10:
- Template: `904`
- Name: Windows10-User-01

Windows 11:
- Template: `905`
- Name: Windows11-User-01

Attach both to:
vmbr2

Start both VMs

---

# Part 2 — Handle First Boot Behavior

## Step 3 — Identify Boot State

When booting the VMs:

- You will NOT land on a Windows desktop
- You will see installation/setup screens

## Step 4 — Understand Why

This happens because:

- Templates are install-ready, not fully installed
- OS setup must be completed manually

---

# Part 3 — Install Windows Server 2022

## Step 5 — Begin Installation

On Primary-Domain-Server:

Select:

Custom: Install Microsoft Server Operating System only (advanced)

## Step 6 — Handle Missing Disk Issue

If no disk appears:

- Click Load Driver
- Browse to VirtIO ISO

Select:

Red Hat VirtIO SCSI controller  
(D:\amd64\2k22\viostor.inf)

## Step 7 — Continue Installation

- Select the disk once visible
- Continue installation
- Allow system to reboot

---

# Part 4 — Initial Server Setup

## Step 8 — Set Administrator Password

Use:

Cyberrange2026

## Step 9 — Log In

Use Proxmox console:

- Click Send Key
- Select Ctrl+Alt+Del

Log in using Administrator

---

# Part 5 — Install VirtIO Drivers

## Step 10 — Identify Missing Drivers

Open Device Manager

Look for:
- Missing Ethernet adapter
- PCI devices

## Step 11 — Install Guest Tools

From VirtIO ISO:

Run:

virtio-win-guest-tools.exe

## Step 12 — Reboot Server

After reboot:

- Network adapter should appear
- No unknown devices should remain

---

# Part 6 — Rename the Server

## Step 13 — Rename Machine

Rename to:

Primary-Domain-Server

Restart system

---

# Part 7 — Configure Static IP

## Step 14 — Set IPv4 Configuration

Configure:

IP Address: 10.20.20.10  
Subnet Mask: 255.255.255.0  
Gateway: 10.20.20.1  
DNS: 127.0.0.1  

## Step 15 — Test Connectivity

Run:

ping 10.20.20.1

If no reply:

- Run: arp -a
- Confirm MAC address exists

Proceed if Layer 2 connectivity is confirmed

---

# Part 8 — Install Active Directory Domain Services

## Step 16 — Open Server Manager

Go to:

Add Roles and Features

## Step 17 — Install Role

Select:

Active Directory Domain Services

Continue through wizard and install

---

# Part 9 — Promote to Domain Controller

## Step 18 — Begin Promotion

Click:

Promote this server to a domain controller

## Step 19 — Choose Deployment Type

Select:

Add a new forest

## Step 20 — Set Domain Name

cyberrange.local

## Step 21 — Configure Options

Keep defaults:

- Forest level: Windows Server 2016
- Domain level: Windows Server 2016
- DNS enabled
- Global Catalog enabled

## Step 22 — Set DSRM Password

Cyberrange2026

## Step 23 — Ignore DNS Warning

Proceed without changes

## Step 24 — Complete Installation

Allow server to reboot

---

# Part 10 — Verify Domain Controller

## Step 25 — Confirm Domain Context

Run:

whoami

Expected:

cyberrange\administrator

## Step 26 — Verify DNS

Open DNS Manager

Confirm:
- cyberrange.local exists
- AD DNS structure present

---

# Part 11 — Create Initial AD Structure

## Step 27 — Open ADUC

Run:

dsa.msc

## Step 28 — Create OUs

Create:

- Employees
- IT
- Servers
- Workstations

---

# Part 12 — Create Admin Account

## Step 29 — Create User

Create:

itadmin

## Step 30 — Configure Password

Cyberrange2026

Set:

- Password never expires
- Do not require change

---

# Part 13 — Prepare Clients for Domain Join

## Step 31 — Configure DNS on Clients

Set DNS:

10.20.20.10

## Step 32 — Test Connectivity

Run:

ping 10.20.20.10  
nslookup cyberrange.local  

---

# Part 14 — Join Clients to Domain

## Step 33 — Join Domain

On each client:

- Open System Properties
- Select Domain
- Enter:

cyberrange.local

## Step 34 — Enter Credentials

cyberrange\itadmin  
Cyberrange2026  

Restart system

---

# Part 15 — Validate Domain Join

## Step 35 — Login Test

Login using:

cyberrange\itadmin

## Step 36 — Verify

Run:

whoami

Confirm domain account

## Step 37 — Verify in AD

Confirm machines appear in AD

## Step 38 — Move Machines

Move from:

Computers

To:

Workstations OU

---

# Final Outcome

At completion:

- Domain Controller is operational
- Active Directory is installed
- DNS is functioning
- Domain authentication works
- Windows clients are domain joined
- Initial OU structure exists

---

# Phase Completion Criteria

Phase 02 is complete when:

- Domain cyberrange.local exists
- AD DS is installed
- DNS is working
- Domain Controller is functional
- Clients can join domain
- Authentication works
- Machines appear in AD
- Workstations are placed in correct OU

---

# Summary

Phase 02 establishes the identity layer of the cyber range.

This phase introduces:

- Active Directory
- DNS
- Domain authentication
- Managed endpoints

At this point, the environment transitions from basic infrastructure into a functioning enterprise system ready for user management, policy enforcement, and expansion.
