## Status

✅ Completed

# Marist SOC Cyber Range
# Lab Build Guide — Phase 01: Infrastructure, Virtualization, and Network Foundation


---

# Purpose

This phase establishes the infrastructure foundation for the entire Marist SOC Cyber Range.

The purpose of this phase is to define and validate the core environment that all later phases depend on. This includes:

- The Proxmox virtualization platform
- The segmented network design
- The firewall and routing layer
- The VM template strategy
- The overall cyber range architecture
- Initial remote access and connectivity validation

Everything built later, including Active Directory, enterprise services, user management, attack simulation, and SOC tooling, depends on the design and decisions made during this phase.

---

# Phase Objectives

By the end of this phase, the environment should have:

- A working Proxmox Virtual Environment server
- Clearly defined network segmentation
- A central firewall and routing layer
- VM templates ready for cloning
- A completed architecture design for the range
- Remote access tested and validated
- Basic familiarity with Proxmox operations

---

# What This Phase Covers

This phase only covers the following topics:

- Infrastructure platform selection and understanding
- Network architecture design
- Firewall and routing role in the environment
- VM template preparation
- Overall cyber range architecture planning
- Remote access and connectivity validation
- Proxmox familiarization
- Core design decisions and lessons learned

This phase does not cover:

- Active Directory deployment
- Domain creation
- User creation
- File server deployment
- SOC tool deployment
- Attack scenario execution

Those belong in later phases.

---

# Environment Overview

## Hypervisor Platform

The cyber range is hosted on a Proxmox Virtual Environment server.

### Node Information

- Node Name: `cyberrange`
- Access Method: Web UI over HTTPS
- Management Interface: Proxmox VE Dashboard

## Role of Proxmox

Proxmox is the main platform used to host and manage the cyber range. In this environment, Proxmox is responsible for:

- Hosting all virtual machines
- Allocating CPU, memory, and storage
- Managing network bridges
- Controlling VM creation, startup, shutdown, and cloning

This means that Proxmox is the foundation layer of the whole project. If the Proxmox configuration is wrong, every later phase will be affected.

---

# Part 1 — Understand the Infrastructure Platform

## Step 1

Identify the hypervisor platform being used for the project.

In this environment, the hypervisor is:

`Proxmox Virtual Environment (PVE)`

This is the system that will host every VM used in the cyber range.

## Step 2

Identify the Proxmox node name.

The node in this project is:

`cyberrange`

This is the main Proxmox system that will appear in the dashboard and serve as the physical host for the range.

## Step 3

Understand how Proxmox is accessed.

The environment is managed through the:

- Proxmox Web UI
- HTTPS-based browser access

This means administrators interact with the environment through the Proxmox dashboard rather than building systems directly on physical hardware.

## Step 4

Understand the role Proxmox plays in the project.

At this stage, make sure everyone on the team understands that Proxmox is responsible for:

- Hosting the virtual machines
- Managing templates
- Assigning resources
- Mapping VMs to the correct network bridges
- Serving as the operational control layer of the cyber range

This understanding is important before any VMs are deployed.

---

# Part 2 — Design the Network Architecture

## Step 5

Define the objective of the network design.

The network must support:

- Realistic enterprise behavior
- Controlled attack and defense workflows
- Isolation between major environments
- Monitoring visibility for the SOC

This means the network cannot be flat. It must be segmented.

## Step 6

Create the Red Team network segment.

Define the following for the Red Team network:

- Subnet: `10.20.10.0/24`
- Proxmox Bridge: `vmbr1`

Purpose of this network:

- Offensive tooling
- Attack simulation
- Red team operations using systems like Kali Linux

This segment represents the attacker side of the range.

## Step 7

Create the Target network segment.

Define the following for the Target network:

- Subnet: `10.20.20.0/24`
- Proxmox Bridge: `vmbr2`

Purpose of this network:

- Enterprise simulation
- User systems
- Servers
- Main attack surface

This segment represents the victim or defended enterprise environment.

## Step 8

Create the SOC / Detection network segment.

Define the following for the SOC / Detection network:

- Subnet: `10.20.30.0/24`
- Proxmox Bridge: `vmbr3`

Purpose of this network:

- Monitoring
- Detection tooling
- Logging and visibility systems

This segment represents the defensive monitoring side of the environment.

## Step 9

Document the final segmented design.

At the end of the network design stage, the environment should be documented as three main zones:

- Red Team → `10.20.10.0/24` on `vmbr1`
- Target → `10.20.20.0/24` on `vmbr2`
- SOC / Detection → `10.20.30.0/24` on `vmbr3`

## Step 10

Understand why segmentation matters.

This design enables:

- Red Team to attack the Target environment
- SOC to monitor the Target environment
- Controlled separation between functional parts of the lab
- More realistic enterprise simulation

This is one of the most important decisions in the entire project because every VM deployed later will rely on this network layout.

---

# Part 3 — Define the Firewall and Routing Layer

## Step 11

Select the firewall and routing platform.

The design uses a firewall/router system such as:

- OPNsense
- pfSense

This system acts as the central control point for traffic between the network segments.

## Step 12

Define the role of the firewall/router.

The firewall/router is responsible for:

- Acting as the default gateway for all subnets
- Routing traffic between the major environments
- Enforcing segmentation policy
- Controlling the flow of attack traffic
- Supporting visibility and analysis

## Step 13

Understand why the firewall/router is necessary.

Without this layer:

- The environment would not behave like a real enterprise network
- There would be less control over traffic paths
- Isolation would be weaker
- Monitoring and scenario design would be harder

This component is critical because it creates realistic network boundaries and supports controlled interaction between Red Team, Target, and SOC environments.

---

# Part 4 — Prepare VM Templates

## Step 14

Identify the available VM templates.

The environment includes the following templates:

- `900 (kali-redteam)`
- `901 (Kali-Purple)`
- `902 (Ubuntu-Server24LTS)`
- `903 (Ubuntu-Desktop24LTS)`
- `904 (Windows-10-EduN)`
- `905 (Windows-11-EduN)`
- `906 (Windows-Server-2022)`

## Step 15

Understand the purpose of templates.

Templates are used so that VMs can be deployed by cloning instead of performing repeated manual installations.

This provides:

- Faster deployment
- Consistency between systems
- Easier scaling
- Fewer configuration mistakes

## Step 16

Adopt the template-based deployment approach.

The standard approach for this cyber range is:

- Build systems by cloning from templates
- Avoid repeated manual base installations whenever possible

This should be treated as a best practice throughout the project.

## Step 17

Confirm the template strategy is ready for later phases.

Before moving on from this phase, ensure the team understands:

- Which templates are available
- What each template is used for
- That future VMs should be built from these templates wherever possible

---

# Part 5 — Design the Cyber Range Architecture

## Step 18

Define the overall objective of the cyber range architecture.

The architecture must support three major functional environments:

- Attackers
- Victims
- Defenders

This means the range is designed as a complete ecosystem, not just a collection of VMs.

## Step 19

Define the Red Team environment.

The Red Team environment includes systems such as:

- Kali Linux machines
- A jump box

Purpose:

- Simulate attacker behavior
- Perform reconnaissance
- Execute exploits and offensive operations

## Step 20

Define the Target environment.

The Target environment includes systems such as:

- Domain Controller
- File server
- Windows endpoints
- Vulnerable applications

Purpose:

- Simulate an enterprise environment
- Generate realistic user and system activity
- Serve as the main attack surface

## Step 21

Define the SOC / Detection environment.

The SOC / Detection environment includes systems such as:

- Security Onion
- Logging tools
- Network monitoring systems

Purpose:

- Detect malicious activity
- Analyze network and host behavior
- Provide defensive visibility into the environment

## Step 22

Understand the architecture outcome.

When combined, these three environments create a full cyber range ecosystem:

- Red Team acts as the attacker
- Target acts as the enterprise victim environment
- SOC acts as the defender and monitoring layer

This architecture is the basis for all later build phases.

---

# Part 6 — Validate Remote Access and Connectivity

## Step 23

Define the goal of connectivity validation.

Before building later phases, confirm that the environment can be accessed and managed remotely.

The goal is to make sure administrators and team members can reliably reach the systems they need.

## Step 24

Verify VPN access into the environment.

Confirm that VPN access works as expected.

This ensures secure remote entry into the cyber range environment.

## Step 25

Test RDP access to Windows systems.

Validate that Remote Desktop access to Windows systems is functional where applicable.

This ensures that Windows systems can be accessed and administered remotely.

## Step 26

Confirm access to the Proxmox Web UI.

Make sure the team can reach the Proxmox dashboard through its web interface.

This is necessary for VM deployment, cloning, and management.

## Step 27

Validate subnet communication.

Confirm that the designed network segments can communicate as intended according to the architecture and routing design.

This does not mean removing segmentation. It means confirming that the intended connectivity model works.

## Step 28

Understand why this validation matters.

This step ensures:

- Remote administration is possible
- Team collaboration is possible
- Troubleshooting can be performed effectively
- The project can continue without basic access issues blocking progress

---

# Part 7 — Build Proxmox Familiarization

## Step 29

Learn the basic Proxmox workflow.

During this phase, the team should become familiar with:

- VM creation
- VM cloning from templates
- Resource allocation
- Network bridge assignment
- Using the console
- Using remote access methods

## Step 30

Understand why Proxmox knowledge matters.

Proxmox is not just where the VMs run. It is the environment’s infrastructure control layer.

Because of that, mistakes in Proxmox can impact:

- VM deployment
- Networking
- Resource stability
- Template usage
- Access and troubleshooting

Team members should be comfortable navigating the platform before moving to later build phases.

---

# Part 8 — Record the Key Design Decisions

## Step 31

Document the decision to use a single Proxmox server.

This design was chosen for:

- Centralized management
- Lower hardware complexity
- Easier maintenance and deployment

## Step 32

Document the decision to use network segmentation.

This design was chosen because it:

- Supports isolation
- Enables realistic attack paths
- Improves scalability
- Matches enterprise design principles

## Step 33

Document the decision to use template-based deployment.

This design was chosen because it:

- Speeds up builds
- Improves consistency
- Reduces manual setup errors

These design decisions should be written down because they explain why the environment was built the way it was.

---

# Part 9 — Record the Key Lessons Learned

## Step 34

Document that planning is critical.

A poorly planned environment creates unnecessary rework later.

This phase shows that infrastructure and network decisions must be made carefully before large-scale VM deployment begins.

## Step 35

Document that network design defines the project.

A weak or unclear network design would limit the realism, security, and usefulness of the cyber range.

Because of that, network architecture is one of the most important elements of the project.

## Step 36

Document that templates are essential.

Templates reduce:

- Build time
- Repeated work
- Configuration inconsistency

They should be treated as a core operational strategy.

## Step 37

Document that hypervisor knowledge is required.

Since all systems depend on Proxmox, understanding the hypervisor is necessary for successful deployment and troubleshooting.

---

# Part 10 — Confirm the Final State of Phase 01

## Step 38

At the end of this phase, verify that the following are true:

- Proxmox environment is operational
- Network segmentation is defined and implemented
- Firewall/routing layer is part of the architecture
- VM templates are available
- Cyber range architecture is fully designed
- Remote access has been validated

## Step 39

Confirm that the infrastructure foundation is ready to support future phases.

The expected result of this phase is not a fully built enterprise network yet.

The expected result is a stable and well-designed infrastructure foundation that can support:

- Identity services
- Endpoint deployment
- Enterprise servers
- Logging and monitoring
- Attack simulation

---

# Quick Reference

## Node

- `cyberrange`

## Networks

- Red Team → `10.20.10.0/24`
- Target → `10.20.20.0/24`
- SOC / Detection → `10.20.30.0/24`

## Proxmox Bridges

- `vmbr1` → Red Team
- `vmbr2` → Target
- `vmbr3` → SOC / Detection

## Templates

- `900 (kali-redteam)`
- `901 (Kali-Purple)`
- `902 (Ubuntu-Server24LTS)`
- `903 (Ubuntu-Desktop24LTS)`
- `904 (Windows-10-EduN)`
- `905 (Windows-11-EduN)`
- `906 (Windows-Server-2022)`

---

# Expected Outcome

By the completion of Phase 01, the cyber range should have:

- A working virtualization platform
- A documented segmented network architecture
- A planned firewall/routing model
- A scalable template strategy
- A clear three-environment architecture
- Verified remote access and management readiness

This means the environment is ready for the next phase of deployment work.

---

# Phase Completion Criteria

Phase 01 is complete when all of the following are true:

- The Proxmox platform is operational
- The node `cyberrange` is accessible
- The three major network zones are defined
- The bridge mappings are documented
- The firewall/routing layer is identified
- The template list is available
- The architecture for Red Team, Target, and SOC is defined
- Remote access has been tested successfully

---

# Transition to Phase 02

The next phase builds on this infrastructure foundation by introducing:

- Windows Server deployment
- Active Directory
- Domain creation
- Endpoint joining

Those tasks are not part of this phase, but this phase makes them possible.

---

# Conclusion

Phase 01 establishes the infrastructure and design foundation of the Marist SOC Cyber Range.

This phase provides the virtualization platform, network segmentation, routing model, template strategy, and architectural planning that everything else depends on.

Without Phase 01, later phases cannot be built reliably.

With Phase 01 complete, the environment is ready to support the structured deployment of enterprise services, endpoints, monitoring systems, and cyber operations.
