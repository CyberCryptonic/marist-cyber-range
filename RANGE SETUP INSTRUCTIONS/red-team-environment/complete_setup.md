# Red Team Environment Setup

This environment simulates the offensive side of the cyber range and is used to launch controlled attacks, generate adversary activity, and support realistic attack-and-defense exercises against the Target Environment.

---

## Status

✅ COMPLETE

The Red Team Environment has been built as the offensive segment of the Marist Cyber Range and is ready to support attack simulation activities.

---

## Build Progress

- ✅ Red Team network segment defined
- ✅ Red Team VM role planning completed
- ✅ Kali Linux attacker systems deployed
- ✅ Instructor attacker system deployed
- ✅ Red Team jump server deployed
- ✅ Network placement configured on Red Team subnet
- ✅ Basic connectivity validated
- ✅ Offensive environment prepared for future scenario execution

---

## Build Order

1. `ip_configuration.md`
2. `phase_01_red_team_networking.md`
3. `phase_02_red_team_attacker_systems.md`
4. `phase_03_red_team_jump_server.md`
5. `phase_04_red_team_validation.md`

---

## Systems Included

### Student Attacker Systems
- Student-Attacker-01 (Kali Linux)
- Student-Attacker-02 (Kali Linux)
- Student-Attacker-03 (Kali Linux)
- Student-Attacker-04 (Kali Linux)
- Student-Attacker-05 (Kali Linux)
- Student-Attacker-06 (Kali Linux)

### Instructor System
- Instructor-Attacker (Kali Linux)

### Red Team Infrastructure
- Red-Team-Jump-Server (Ubuntu Server)

---

## Network Design Notes

- The Red Team Environment is placed on its own isolated subnet
- Red Team subnet: `10.20.10.0/24`
- Proxmox bridge: `vmbr1`
- The Red Team environment represents the attacker side of the cyber range
- This segment is separated from the Target and SOC environments to preserve controlled attack paths
- Systems in this segment are used to initiate offensive activity, testing, and scenario execution
- IP assignments for all Red Team machines should be documented in the Red Team IP configuration file
- Static addressing is recommended for attacker and jump systems so they remain predictable during exercises

---

## Current Completion State

The Red Team Environment is operational and ready to support controlled offensive simulation inside the cyber range.

All systems are:

- Built and configured
- Attached to the correct Red Team network
- Functionally validated for internal communication
- Prepared for use in future attack scenarios

---

### Completed

- Red Team subnet defined and implemented
- Student attacker systems deployed
- Instructor attacker system deployed
- Red Team jump server deployed
- Kali Linux offensive workstations prepared
- Ubuntu jump server prepared
- Internal Red Team connectivity validated
- Red Team environment aligned with overall cyber range topology

---

### In Progress

None

---

## Next Phase

Red Team scenario preparation and offensive tooling validation

This phase may include:

- attacker tool verification
- SSH access validation
- package updates
- offensive tool installation or confirmation
- jump server usage testing
- controlled connectivity testing into allowed target paths

---

## Goal

To replicate a realistic attacker environment that supports:

- offensive security training
- controlled attack simulation
- red team operations
- adversary emulation against the Target Environment

This environment serves as the offensive segment of the cyber range and is used to generate the attack activity that the Target and SOC environments will later detect, investigate, and respond to.

---

# Marist SOC Cyber Range
# Lab Build Guide — Red Team Environment Setup

---

# Purpose

This phase establishes the Red Team Environment for the Marist Cyber Range.

The purpose of this environment is to provide a dedicated offensive network segment where attacker systems can be deployed, managed, and used during controlled cyber exercises. This environment is intentionally separated from the Target and SOC environments so the cyber range can model realistic attack paths while still maintaining structure and control.

By the end of this setup, the Red Team Environment should provide:

- multiple student attacker workstations
- one instructor attacker workstation
- one jump server for controlled access and staging
- a clean offensive subnet for attack simulation
- a repeatable platform for future scenarios and demonstrations

---

# Environment Overview

The Red Team Environment is the attacker side of the cyber range.

It is used to simulate:

- student-led offensive activity
- instructor-led offensive demonstrations
- attack path development
- reconnaissance and exploitation workflows
- adversary behavior for SOC monitoring exercises

This environment is not meant to function like an enterprise business network. Instead, it functions as the source of offensive operations directed toward the Target Environment under controlled conditions.

---

# Phase Objectives

By the end of this phase, the environment should have:

- a working Red Team subnet
- six student Kali Linux attacker systems
- one instructor Kali Linux attacker system
- one Ubuntu Server jump server
- all Red Team systems connected to the correct Proxmox bridge
- hostnames assigned correctly
- network communication validated
- the Red Team environment ready for future scenario execution

---

# Systems Built in This Phase

## Kali Linux Systems

- `Student-Attacker-01`
- `Student-Attacker-02`
- `Student-Attacker-03`
- `Student-Attacker-04`
- `Student-Attacker-05`
- `Student-Attacker-06`
- `Instructor-Attacker`

## Ubuntu Server System

- `Red-Team-Jump-Server`

---

# Part 1 — Define the Red Team Network

## Step 1 — Identify the Red Team subnet

The Red Team subnet for this project is:

`10.20.10.0/24`

This subnet is reserved for attacker infrastructure only.

---

## Step 2 — Identify the correct Proxmox bridge

The Red Team network is attached to:

`vmbr1`

Every Red Team virtual machine must use this bridge so it is placed on the correct network segment.

---

## Step 3 — Understand the purpose of this segment

This segment exists to provide a dedicated attacker environment that is logically separated from:

- the Target Environment
- the SOC / Detection Environment

This separation is important because it preserves realism and prevents the lab from becoming a flat network.

---

# Part 2 — Prepare for VM Deployment

## Step 4 — Identify the VM templates used

The Red Team systems use the following base templates:

- `900 (kali-redteam)`
- `902 (Ubuntu-Server24LTS)`

These templates are used so the Red Team environment can be built quickly and consistently through cloning.

---

## Step 5 — Confirm naming standards

Use consistent names for all Red Team systems.

The systems in this environment should be named:

- `Student-Attacker-01`
- `Student-Attacker-02`
- `Student-Attacker-03`
- `Student-Attacker-04`
- `Student-Attacker-05`
- `Student-Attacker-06`
- `Instructor-Attacker`
- `Red-Team-Jump-Server`

Consistent naming makes management, documentation, and troubleshooting much easier later.

---

# Part 3 — Build the Student Attacker Systems

## Step 6 — Clone the first student attacker VM

In Proxmox:

- Select template: `900 (kali-redteam)`
- Clone the template
- Name the VM:

`Student-Attacker-01`

- Attach the NIC to:

`vmbr1`

- Start the VM

---

## Step 7 — Complete first-boot configuration

On first boot of the Kali system:

- complete any required initial setup
- confirm the hostname
- confirm the local user account
- confirm the system reaches the desktop or shell properly

If the hostname is not already correct, change it to:

`Student-Attacker-01`

Reboot if necessary.

---

## Step 8 — Configure network settings

Assign the system its intended Red Team IP settings according to your Red Team IP configuration document.

Confirm:

- the system is on `10.20.10.0/24`
- the network interface is active
- the correct gateway is set if your design requires one
- the system can communicate on the Red Team subnet

Static IP addressing is recommended for attacker systems so they remain stable across exercises.

---

## Step 9 — Update and validate the system

Open a terminal and run:

`sudo apt update`
`sudo apt upgrade -y`

Then verify:

- hostname is correct
- interface is up
- IP addressing is correct
- basic connectivity works

---

## Step 10 — Repeat for the remaining student attacker systems

Repeat the cloning and setup process for:

- `Student-Attacker-02`
- `Student-Attacker-03`
- `Student-Attacker-04`
- `Student-Attacker-05`
- `Student-Attacker-06`

For each one:

- clone from `900 (kali-redteam)`
- connect NIC to `vmbr1`
- assign the correct hostname
- configure the planned Red Team IP address
- validate connectivity

At the end of this step, all six student attacker systems should exist and be network connected.

---

# Part 4 — Build the Instructor Attacker System

## Step 11 — Clone the instructor attacker VM

In Proxmox:

- Select template: `900 (kali-redteam)`
- Clone the template
- Name the VM:

`Instructor-Attacker`

- Attach the NIC to:

`vmbr1`

- Start the VM

---

## Step 12 — Complete first-boot setup

On the Kali system:

- complete any required initial setup
- confirm the hostname
- confirm the login works properly

Set or verify the hostname as:

`Instructor-Attacker`

Reboot if necessary.

---

## Step 13 — Configure networking

Assign the instructor system its intended Red Team IP configuration.

Confirm:

- it is on the Red Team subnet
- it can communicate with the other attacker systems
- it is documented in the Red Team IP addressing file

This system is intended for instructor-led demonstrations, validation, and scenario control.

---

## Step 14 — Update and validate the system

Run:

`sudo apt update`
`sudo apt upgrade -y`

Then verify:

- hostname is correct
- IP addressing is correct
- the system can reach other Red Team systems where expected

---

# Part 5 — Build the Red Team Jump Server

## Step 15 — Clone the jump server VM

In Proxmox:

- Select template: `902 (Ubuntu-Server24LTS)`
- Clone the template
- Name the VM:

`Red-Team-Jump-Server`

- Attach the NIC to:

`vmbr1`

- Start the VM

---

## Step 16 — Complete Ubuntu Server first-boot setup

On first boot:

- complete any required setup
- set or confirm the hostname
- confirm the administrative account
- confirm login works from the console

Set the hostname to:

`Red-Team-Jump-Server`

Reboot if necessary.

---

## Step 17 — Configure network settings

Assign the jump server its intended static Red Team IP configuration.

Confirm:

- the interface is active
- the server is on `10.20.10.0/24`
- the address is documented properly
- internal Red Team communication works

Because this is infrastructure inside the Red Team segment, static addressing should be used.

---

## Step 18 — Update the jump server

Run:

`sudo apt update`
`sudo apt upgrade -y`

This ensures the jump server begins from a stable and updated baseline.

---

## Step 19 — Verify server readiness

Confirm the following on the jump server:

- hostname is correct
- IP addressing is correct
- basic internal network connectivity works
- the system boots and logs in normally

This machine acts as Red Team support infrastructure and may later be used for staging, access management, tool hosting, or instructor-controlled coordination.

---

# Part 6 — Validate the Red Team Environment

## Step 20 — Verify all Red Team systems exist in Proxmox

In Proxmox, confirm the following VMs are present and operational:

- `Student-Attacker-01`
- `Student-Attacker-02`
- `Student-Attacker-03`
- `Student-Attacker-04`
- `Student-Attacker-05`
- `Student-Attacker-06`
- `Instructor-Attacker`
- `Red-Team-Jump-Server`

Each VM should be attached to `vmbr1`.

---

## Step 21 — Verify hostnames

On each VM, confirm the hostname matches the intended system name.

This is important for documentation consistency and later scenario coordination.

---

## Step 22 — Verify IP configuration

On each VM, verify:

- it has the correct planned IP address
- it is on the Red Team subnet
- there are no duplicate addresses
- the addressing matches the Red Team IP configuration documentation

---

## Step 23 — Verify internal Red Team communication

Test communication between Red Team systems where appropriate.

Examples:

- attacker system to attacker system
- attacker system to jump server
- instructor system to jump server

This confirms the Red Team segment is functioning internally.

---

## Step 24 — Verify system stability

For each VM, confirm:

- the system boots correctly
- the network interface remains active
- login works properly
- there are no major configuration issues

---

## Step 25 — Record final completion state

At the end of validation, the Red Team environment should now contain:

- six student Kali Linux attacker systems
- one instructor Kali Linux attacker system
- one Ubuntu Server jump server
- a functioning offensive subnet
- stable internal Red Team connectivity

At this point, the Red Team segment is considered built and ready for later scenario usage.

---

# Expected Results

By the end of the Red Team Environment setup:

- all Red Team VMs are deployed
- all systems are connected to `vmbr1`
- all systems are placed on `10.20.10.0/24`
- hostnames are correctly assigned
- student attacker systems are operational
- instructor attacker system is operational
- jump server is operational
- internal Red Team connectivity is validated

---

# Key Concepts

- the Red Team environment is the offensive segment of the lab
- Kali Linux systems provide attacker workstations
- the jump server provides supporting Red Team infrastructure
- segmentation matters because it preserves realism and control
- documentation consistency matters for troubleshooting and future scenario building

---

# Common Mistakes to Avoid

- attaching Red Team systems to the wrong Proxmox bridge
- forgetting to rename cloned systems
- reusing duplicate IP addresses
- failing to document assigned IPs
- assuming a VM is complete without verifying connectivity
- mixing Red Team systems into the Target or SOC subnet

---

# Phase Completion Criteria

The Red Team Environment setup is complete when all of the following are true:

- the Red Team subnet is functioning
- all six student attacker VMs are deployed
- the instructor attacker VM is deployed
- the Red Team jump server is deployed
- every Red Team VM is attached to `vmbr1`
- hostnames are correct
- IP assignments are correct
- internal Red Team connectivity has been validated

---

# Transition to the Next Phase

After this phase is complete, the Red Team environment can be used for:

- attack scenario execution
- offensive tooling validation
- adversary emulation
- controlled testing against the Target Environment
- SOC detection exercises

---

# Summary

The Red Team Environment provides the offensive side of the Marist Cyber Range.

This setup establishes a dedicated attacker subnet containing multiple Kali Linux systems for student and instructor use, along with a Red Team jump server for supporting infrastructure. With this environment in place, the cyber range now has a structured offensive segment that can be used to generate realistic attacker activity for training, demonstrations, and future attack-and-defense workflows.
