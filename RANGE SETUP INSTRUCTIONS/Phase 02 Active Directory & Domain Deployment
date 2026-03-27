# Marist SOC Cyber Range
# Lab Build Guide — Phase 02: Active Directory Deployment and Domain Setup

## Purpose

This document explains, in detail, how the Marist SOC Cyber Range moved from a base Proxmox infrastructure into a functioning Windows enterprise domain environment.

This phase focused on:

- Cloning the core Windows systems from Proxmox templates
- Installing Windows where required
- Installing VirtIO drivers
- Configuring the first server as the Domain Controller
- Installing Active Directory Domain Services (AD DS)
- Creating the `cyberrange.local` domain
- Configuring DNS
- Joining Windows 10 and Windows 11 workstations to the domain
- Creating the initial Active Directory structure for future management

The outcome of this phase was a working domain environment that future students can expand with users, servers, Group Policy, logging, and SOC tooling.

---

# 1. Phase Objective

The objective of Phase 02 was to establish the identity and authentication backbone of the cyber range.

Before this phase, the environment only consisted of infrastructure and networking. After this phase, the environment contained:

- A functioning Domain Controller
- Active Directory
- DNS integrated with AD
- Domain-based authentication
- Domain-joined Windows endpoints

This is the point where the project stopped being "just virtual machines" and started behaving like a real enterprise network.

---

# 2. Systems Used in This Phase

## Proxmox Templates Used

The following templates were provided and used for cloning:

- `904 (Windows-10-EduN)`
- `905 (Windows-11-EduN)`
- `906 (Windows-Server-2022)`

## Virtual Machines Built

### Target Environment
All three of the following systems were placed on the Target network (`vmbr2` / `10.20.20.0/24`):

- `Primary-Domain-Server`
- `Windows10-User-01`
- `Windows11-User-01`

## Why these systems were chosen first

The full topology contains many more machines, but this phase intentionally started small.

These three systems were enough to establish:

- a domain
- centralized authentication
- two managed workstations
- the foundation for later attack and defense scenarios

This prevented unnecessary complexity early in the project.

---

# 3. Proxmox Network Placement

## Network Mapping Used

The project network bridges were already established in Proxmox as follows:

- `vmbr1` → Red Team
- `vmbr2` → Target Environment
- `vmbr3` → SOC / Detection

For Phase 02, all Windows systems were deployed to:

- `vmbr2`

## Why vmbr2 was used

The systems built in this phase represented the internal enterprise environment. Since the Domain Controller and workstations belong to the target enterprise network, they needed to live on the Target bridge.

---

# 4. VM Cloning Process

## Systems cloned

### Domain Controller
- Template: `906 (Windows-Server-2022)`
- Proxmox VM Name: `Primary-Domain-Server`

### Windows 10 Workstation
- Template: `904 (Windows-10-EduN)`
- Proxmox VM Name: `Windows10-User-01`

### Windows 11 Workstation
- Template: `905 (Windows-11-EduN)`
- Proxmox VM Name: `Windows11-User-01`

## Important observation after cloning

When these machines were first started, they did not boot directly into a finished Windows desktop environment. Instead, they booted into Windows installation / setup screens.

## Why this happened

Although these systems were provided as templates, they still required Windows installation steps and driver loading before the operating systems were usable.

This is important for future students to understand:

- do not assume a Proxmox template is fully ready-to-use
- always verify whether the template is a preinstalled image or an install-ready template

---

# 5. First Boot Troubleshooting

## Boot issue encountered

When first powering on the Windows systems, boot menus / installation screens appeared instead of a normal Windows login desktop.

## Root cause

The template state indicated that the systems still needed:

- Windows installation completion
- proper VirtIO storage driver support
- proper VirtIO network driver installation after OS setup

## Important lesson

This was not a Proxmox failure. It simply meant the workflow had to include full OS setup.

---

# 6. Installing Windows Server 2022 on Primary-Domain-Server

## Installation path chosen

Once the Windows Server installer loaded, the correct installation option selected was:

- `Custom: Install Microsoft Server Operating System only (advanced)`

## Why "Upgrade" was not used

The "Upgrade" option only works when Windows is already installed on the machine. Since this was effectively a fresh installation on a virtual disk, "Custom" was the correct choice.

---

# 7. Loading the VirtIO Storage Driver During Windows Server Install

## Problem encountered

During installation, Windows Server setup did not initially see the VM disk.

## Why

The VM disk was using VirtIO storage. Windows does not always include the necessary VirtIO storage driver by default during setup.

## Fix applied

The VirtIO ISO was already attached to the VM, so the correct driver was loaded manually from the installation wizard.

## Driver selected

The correct driver selected was:

- `Red Hat VirtIO SCSI controller (D:\amd64\2k22\viostor.inf)`

## Why this driver was chosen

The operating system being installed was Windows Server 2022, so the `2k22` version of the VirtIO storage driver was the correct match.

## Result

After loading this driver:

- the VM disk became visible
- Windows Server installation continued normally

---

# 8. Completing Windows Server Installation

## Basic installation completion

After the disk became visible:

- the target disk was selected
- Windows installation was allowed to continue
- the system copied files and rebooted automatically

## Initial administrator password

An administrator password was set during installation.

For lab consistency, a standardized password convention was chosen for the environment:

- `Cyberrange2026`

## Why a standard password was used

Because this is a controlled training environment, simplicity and consistency were prioritized over production-style password hygiene.

This helps reduce:
- lockouts
- confusion
- unnecessary troubleshooting during demonstrations and testing

---

# 9. Sending Ctrl+Alt+Del in Proxmox

## Problem encountered

After installation, the Windows login screen required `Ctrl + Alt + Del`, but pressing that combination on the physical keyboard affected the local laptop instead of the VM.

## Why

Proxmox console sessions do not pass secure attention sequences directly from the local machine keyboard in the normal way.

## Correct solution

The Proxmox console's built-in key sending function was used:

- `Send Key → Ctrl+Alt+Del`

## Important note for future students

Whenever Windows in Proxmox requires `Ctrl + Alt + Del`, always use the Proxmox console key menu instead of your physical keyboard.

---

# 10. Installing VirtIO Drivers Inside Windows Server

## Network problem encountered

After logging into Windows Server, no Ethernet adapter appeared in Network Connections.

## Why

Although the operating system was installed, the VirtIO network adapter driver was still missing.

## How this was identified

In Device Manager, unknown / missing devices appeared, including:

- Ethernet-related devices
- PCI device entries
- PCI Simple Communications Controller entries

## Initial partial fix

The VirtIO Ethernet driver was installed so that Windows Server could recognize the NIC.

## Full fix applied

Instead of manually loading every missing driver one by one, the full VirtIO guest tools installer was used from the attached VirtIO ISO.

### Installer used
- `virtio-win-guest-tools.exe`

## Result

This installed:
- NIC drivers
- guest communication drivers
- additional VirtIO-related system drivers
- PCI-related drivers

After installation and reboot:
- the Ethernet adapter appeared correctly
- missing devices were resolved
- the machine was ready for network configuration

---

# 11. Renaming the Server

## Server hostname decision

The in-guest server name was kept as:

- `Primary-Domain-Server`

## Why this name was kept

Although a shorter industry-style name such as `DC01` was considered, the final decision was to keep the longer topology-aligned name for clarity and consistency with the project documentation and diagrams.

This is acceptable in a lab environment as long as naming remains consistent everywhere.

---

# 12. Configuring Static IP on the Domain Controller

## Why static IP was required

A Domain Controller must have a predictable IP address. Clients need a stable DNS target, and the Domain Controller itself must reliably know its own network identity.

## Final IPv4 configuration used

On `Primary-Domain-Server`, the following IPv4 configuration was applied:

- IP Address: `10.20.20.10`
- Subnet Mask: `255.255.255.0`
- Default Gateway: `10.20.20.1`
- Preferred DNS: `127.0.0.1`

## Why DNS was set to 127.0.0.1

This machine was about to become its own DNS server as part of Active Directory installation. Pointing DNS to localhost is normal and appropriate for a Domain Controller once DNS is installed locally.

---

# 13. Gateway Connectivity Testing on the Domain Controller

## Ping test result

A ping to the default gateway (`10.20.20.1`) initially timed out.

## Investigation performed

The `arp -a` command was used to inspect the ARP cache.

## Result observed

The ARP table showed a MAC address associated with `10.20.20.1`.

## Meaning of this result

This proved that:

- the server was on the correct network
- the bridge assignment was correct
- the gateway device existed on the subnet
- Layer 2 communication was functioning

The likely issue was only that the gateway/firewall was not responding to ping (ICMP) rather than a full connectivity failure.

## Decision made

The build continued, because local subnet communication and domain functionality could still proceed successfully.

---

# 14. Installing Active Directory Domain Services (AD DS)

## Starting point

Server Manager was opened on `Primary-Domain-Server`.

## Role installation steps followed

1. Open `Server Manager`
2. Click `Add roles and features`
3. Select `Role-based or feature-based installation`
4. Confirm the current server is selected
5. Check:
   - `Active Directory Domain Services`
6. Accept automatically added features
7. Proceed through the wizard
8. Install the role

## Important note about the Features page

No extra boxes needed to be manually selected on the Features page.

### Why

Windows automatically selected all required dependencies when AD DS was chosen.

---

# 15. Promoting the Server to a Domain Controller

## Promotion step

After role installation completed, the post-installation task was launched:

- `Promote this server to a domain controller`

## Deployment configuration selected

The correct option chosen was:

- `Add a new forest`

## Why

This was the very first Domain Controller in the environment. There was no existing domain to join.

## Root domain name created

The following domain was created:

- `cyberrange.local`

## Domain controller options kept

The following defaults were kept:

- Forest functional level: `Windows Server 2016`
- Domain functional level: `Windows Server 2016`
- DNS Server: enabled
- Global Catalog: enabled
- Read-only Domain Controller: disabled

## DSRM password

A Directory Services Restore Mode password was configured using the lab standard:

- `Cyberrange2026`

## DNS warning behavior

A DNS delegation warning appeared during the wizard.

### Decision

This warning was ignored, because it is normal in a lab where there is no preexisting parent DNS infrastructure.

## Paths

All AD database, log, and SYSVOL paths were left at default values.

## Result

The server completed promotion and rebooted automatically.

---

# 16. Verifying Domain Controller Success

After reboot, several checks were performed.

## Authentication verification

The following command was used:

- `whoami`

It returned:

- `cyberrange\administrator`

### Meaning

This confirmed:
- the machine was now operating in the domain context
- Active Directory was functioning
- the server was successfully promoted

---

## DNS verification

DNS Manager was opened and the following were confirmed:

- `cyberrange.local`
- host records for the server
- AD-related DNS folders
- internal AD-integrated DNS structure

### Meaning

This confirmed:
- DNS was installed correctly
- AD and DNS integration was healthy
- the Domain Controller was registering itself in DNS

---

# 17. Creating the Initial Active Directory Structure

## OUs created

The following Organizational Units were created under `cyberrange.local`:

- `Employees`
- `IT`
- `Servers`
- `Workstations`

## Intended additional OU

A `Groups` OU was also identified as necessary for later clean administration, although it had not yet been created at the time this work session paused.

## Why OUs were created

OUs were created to provide clean administrative structure and prepare the environment for:

- user placement
- machine placement
- security group organization
- future Group Policy application

Without OUs, the environment would remain difficult to manage and scale.

---

# 18. Creating the Domain Admin User

## Account created

A dedicated administrative account was created for domain operations:

- `itadmin`

## Password used

- `Cyberrange2026`

## Password-related settings chosen

For this lab environment, the following approach was adopted:

- `Password never expires` → enabled
- `User must change password at next logon` → disabled

## Why

This was done to avoid:
- password expiration breaking the lab
- repeated admin lockouts
- unnecessary interruptions during build and demo work

## Initial location of the account

The account initially existed in the default:

- `Users` container

## Important note

The default `Users` container is not ideal for long-term organization because it is not a custom OU.

## Intended improvement

The `itadmin` user should later be moved into:

- `IT` OU

and then added to a purpose-built security group such as:

- `IT-Admins`

---

# 19. Preparing Windows 10 for Domain Join

## Windows 10 system built

The Windows 10 VM cloned from template `904` was configured next.

## In-guest hostname used

The workstation hostname used was:

- `WIN10-USER-01`

## Why this hostname format was used

This naming approach kept the VM easy to identify while remaining more Windows-friendly than longer descriptive phrases.

## Static network configuration applied

Windows 10 was configured with:

- IP Address: `10.20.20.20`
- Subnet Mask: `255.255.255.0`
- Default Gateway: `10.20.20.1`
- Preferred DNS: `10.20.20.10`

## Why DNS pointed to 10.20.20.10

Clients must use the Domain Controller as their DNS server in order to locate the domain and domain services.

## Connectivity verification

The following checks were performed successfully:

- ping to `10.20.20.10`
- `nslookup cyberrange.local`

## Meaning

This confirmed:
- the client could see the Domain Controller
- DNS was correctly configured
- the system was ready for a domain join

---

# 20. Joining Windows 10 to the Domain

## Domain join steps followed

On Windows 10:

1. Open system properties
2. Open the rename / domain membership dialog
3. Select `Domain`
4. Enter:
   - `cyberrange.local`
5. Provide credentials:
   - `cyberrange\itadmin`
   - `Cyberrange2026`

## Result

The machine successfully joined the domain and rebooted.

## Login verification

After reboot, login was performed using:

- `cyberrange\itadmin`

and `whoami` returned:

- `cyberrange\itadmin`

## Meaning

This confirmed:
- the machine joined the domain successfully
- domain-based authentication worked correctly

## AD verification

The computer object for the workstation appeared in Active Directory.

## Organizational cleanup

The workstation was moved from the default `Computers` container into the:

- `Workstations` OU

## Why that move was correct

The default `Computers` container is only a generic holding location. Workstations should be placed into a dedicated OU for organization and future Group Policy targeting.

---

# 21. Preparing Windows 11 for Domain Join

## Windows 11 system built

The Windows 11 VM cloned from template `905` was configured next.

## In-guest hostname used

The workstation hostname used was:

- `WIN11-USER-01`

## Static network configuration applied

Windows 11 was configured with:

- IP Address: `10.20.20.21`
- Subnet Mask: `255.255.255.0`
- Default Gateway: `10.20.20.1`
- Preferred DNS: `10.20.20.10`

## Connectivity verification

The workstation successfully pinged:

- `10.20.20.10`

This confirmed it could communicate with the Domain Controller.

---

# 22. Joining Windows 11 to the Domain

## Domain join steps followed

On Windows 11:

1. Open system properties / domain membership settings
2. Select `Domain`
3. Enter:
   - `cyberrange.local`
4. Authenticate with:
   - `cyberrange\itadmin`
   - `Cyberrange2026`

## Result

The machine successfully joined the domain and rebooted.

## Login verification

After reboot, login was performed using the same domain admin account.

This confirmed:
- domain authentication worked correctly on the second workstation
- the Windows 11 system was properly integrated into the enterprise environment

## AD verification

The workstation appeared in Active Directory and was moved into the:

- `Workstations` OU

---

# 23. Active Directory State at the End of Phase 02

By the end of this phase, Active Directory contained:

## Core Infrastructure
- `Primary-Domain-Server` functioning as Domain Controller
- AD-integrated DNS
- domain: `cyberrange.local`

## Administrative Identity
- `itadmin`

## Organizational Units
- `Employees`
- `IT`
- `Servers`
- `Workstations`

## Managed Workstations
- `WIN10-USER-01`
- `WIN11-USER-01`

Both workstations:
- joined the domain
- authenticated successfully
- appeared in Active Directory
- were moved into the `Workstations` OU

---

# 24. Key Technical Lessons Learned

## 1. Templates may still require installation
Future students should verify the state of cloned templates immediately. A template may still require OS installation steps.

## 2. VirtIO drivers are essential in Proxmox
Windows guests often require:
- storage drivers during installation
- guest tools after installation
- network drivers before network configuration will work

## 3. DNS is the key dependency for domain joining
If a workstation cannot resolve the domain through the Domain Controller, the join will fail even if general IP connectivity looks correct.

## 4. The default Users and Computers containers are only starting points
For proper management and later policy application, build out dedicated OUs early and move machines / users into them.

## 5. Lab simplicity is acceptable when intentional
Using one standardized password (`Cyberrange2026`) is acceptable in a teaching lab when the goal is reliability and repeatability, not production security.

---

# 25. Final Outcome of Phase 02

At the end of this phase, the Marist SOC Cyber Range had a functioning enterprise identity environment.

This included:

- a working Domain Controller
- a functioning internal DNS server
- an Active Directory domain
- domain authentication
- two managed domain-joined Windows endpoints
- an initial OU structure for future expansion

This completed the foundational identity layer of the cyber range and prepared the project for the next phase:
- users
- groups
- Group Policy
- logging
- servers
- SOC tooling
- attack simulations

---

# 26. Quick Reference

## Domain
- `cyberrange.local`

## Standard Lab Password
- `Cyberrange2026`

## Systems
- `Primary-Domain-Server` → `10.20.20.10`
- `WIN10-USER-01` → `10.20.20.20`
- `WIN11-USER-01` → `10.20.20.21`

## Network
- Bridge: `vmbr2`
- Subnet: `10.20.20.0/24`
- Gateway: `10.20.20.1`

## OUs Created
- `Employees`
- `IT`
- `Servers`
- `Workstations`

---

# 27. Recommended Next Steps

The next phase should include:

## Directory Structure Completion
- Create `Groups` OU
- Create security groups such as `IT-Admins`
- Move `itadmin` into the `IT` OU
- Add `itadmin` to `IT-Admins`

## User Buildout
- Create standard employee accounts in `Employees`
- Assign passwords and stable settings for lab use

## Policy and Control
- Begin Group Policy design
- Apply workstation management policies through the `Workstations` OU

## Range Expansion
- Build additional servers
- Add vulnerable applications
- Deploy SOC and logging tools

---

# Conclusion

Phase 02 transformed the cyber range from a base virtual environment into a functioning Windows enterprise domain. With Active Directory, DNS, centralized authentication, and two managed workstations now operational, the project gained the core identity and management structure required for realistic cyber operations, enterprise administration, and future attack-and-defense scenarios.
