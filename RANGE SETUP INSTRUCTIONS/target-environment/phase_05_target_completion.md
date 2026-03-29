## Status

✅ Completed

- Backup Domain Server deployed and validated
- Internal Web Server deployed and validated
- Windows Log Server deployed and prepared
- IT Admin Workstation deployed and operational
- Incident Response Workstation deployed and operational
- Vulnerable Training Server deployed and accessible
- Blue Team Analysis Workstation (Kali Purple) operational
- Full Target Environment validation completed

---

# Marist SOC Cyber Range
# Lab Build Guide — Phase 05: Target Environment Completion

---

# Purpose

Phase 05 completes the remaining systems required to make the Target Environment behave like a realistic enterprise network.

This phase adds the remaining infrastructure, administrative systems, defensive workstations, and vulnerable services that were planned in the topology but not yet built during earlier phases.

By the end of this phase, the Target Environment will include:

- Redundant domain infrastructure
- Internal web services
- Centralized Windows log collection preparation
- Administrative management systems
- Incident response tooling
- Vulnerable application targets
- Blue team analysis capability

This phase is completed before SOC/Detection setup so the environment is fully built and producing realistic activity before monitoring is introduced.

---

# Objectives

- Build the Backup Domain Server
- Build the Internal Web Server
- Build the Windows Log Server
- Build the IT Admin Workstation
- Build the Incident Response Workstation
- Build the Vulnerable Training Server
- Build the Blue Team Analysis Workstation (Kali Purple)
- Validate that all Target Environment systems function correctly

---

# Prerequisites

Before beginning this phase, the following should already be complete:

- Proxmox environment operational
- Target network functioning on `10.20.20.0/24`
- Primary Domain Controller operational
- Domain `cyberrange.local` functioning
- Windows 10 and Windows 11 domain clients working
- File Server working
- Active Directory structure in place
- Group Policy functioning
- Basic file access already validated

---

# Recommended Build Order

Build the remaining Target Environment systems in this order:

1. Backup Domain Server
2. Internal Web Server
3. Windows Log Server
4. IT Admin Workstation
5. Incident Response Workstation
6. Vulnerable Training Server
7. Blue Team Analysis Workstation (Kali Purple)
8. Final validation testing

This order matters because some later systems depend on domain services, DNS, or the general enterprise environment already being stable.

---

# Network Placement

All systems in this phase belong to the Target Environment unless your topology states otherwise.

Target network details:

- Subnet: `10.20.20.0/24`
- Gateway: `10.20.20.1`
- Domain Controller / DNS: `10.20.20.10`

Every Windows system that joins the domain should use the domain DNS server.

---

# Part 1 — Build the Backup Domain Server

# Purpose

The Backup Domain Server adds redundancy to the domain environment. If the primary domain controller is unavailable, the environment still has another domain controller that can continue supporting authentication and directory services.

---

## Step 1 — Create the VM in Proxmox

In Proxmox:

- Create a new VM or clone from the Windows Server 2022 template
- Assign the VM a clear name such as:

`Backup-Domain-Server`

- Attach the VM NIC to the Target bridge / Target network
- Allocate CPU, RAM, and storage according to your project standards
- Start the VM

---

## Step 2 — Complete Windows Installation if Needed

If the server boots into Windows setup instead of a desktop:

- Continue the Windows Server installation
- If the disk is not visible, load the VirtIO storage driver from the VirtIO ISO
- Complete installation
- Set the local Administrator password

Use your lab standard password if that is what your project is using consistently

---

## Step 3 — Install VirtIO Drivers

Once logged into Windows Server:

- Open Device Manager
- Check for missing devices
- Run the VirtIO guest tools installer if required
- Reboot after installation

Confirm:
- Network adapter appears
- No major missing devices remain

---

## Step 4 — Rename the Server

Rename the server to:

`Backup-Domain-Server`

Restart after renaming

---

## Step 5 — Assign a Static IPv4 Address

Set a static address on the Target subnet.

Use an unused address in the Target server range.

Example format:

- IP address: choose an unused `10.20.20.x`
- Subnet mask: `255.255.255.0`
- Default gateway: `10.20.20.1`
- Preferred DNS: `10.20.20.10`

Important:
- Do not use DHCP for a domain controller
- DNS should point to the current functioning domain controller during join and promotion steps

---

## Step 6 — Verify Basic Connectivity

Open Command Prompt and test:

- Ping the Primary Domain Controller
- Ping the File Server
- Ping the gateway

Then test name resolution:

- `nslookup cyberrange.local`

Do not continue until:
- IP connectivity works
- DNS resolves correctly

---

## Step 7 — Join the Backup Server to the Domain

Open System Properties or Server Manager and join the machine to:

`cyberrange.local`

Use domain administrative credentials when prompted

Restart after the join completes

---

## Step 8 — Verify the Domain Join

After reboot:

- Log in with a domain administrative account
- Confirm the computer object appears in Active Directory
- Move the server into the correct OU if needed

---

## Step 9 — Install Active Directory Domain Services

On the Backup Domain Server:

- Open Server Manager
- Select Add Roles and Features
- Install:

`Active Directory Domain Services`

Proceed through the wizard and install the role

---

## Step 10 — Promote the Server to a Domain Controller

After role installation:

- Click the post-installation task notification
- Select:

`Promote this server to a domain controller`

This time, do not create a new forest

Choose the option to:

- Add a domain controller to an existing domain

Domain:
`cyberrange.local`

Enter domain admin credentials if prompted

---

## Step 11 — Configure Domain Controller Options

During promotion:

- Keep DNS enabled if offered
- Keep Global Catalog enabled
- Do not select Read Only Domain Controller
- Set the DSRM password

Use your lab standard if you are keeping consistency

Proceed through the wizard

Any delegation warning that is normal in your lab can be reviewed and continued past if appropriate

---

## Step 12 — Complete Promotion and Reboot

Finish the wizard and allow the system to reboot

This may take several minutes

---

## Step 13 — Verify Replication and DC Health

After reboot:

Log into the server and verify:

- `whoami` shows domain context
- Active Directory tools open correctly
- DNS Manager opens correctly

Then run:

- `repadmin /replsummary`
- `dcdiag`

You want:
- No major replication failures
- No critical AD failures

---

## Step 14 — Verify the Backup DC in Active Directory

On either domain controller:

- Open Active Directory Users and Computers
- Confirm Backup-Domain-Server exists
- Confirm the Domain Controllers OU reflects the added controller if applicable
- Confirm DNS records exist for the new controller

---

## Step 15 — Perform a Basic Redundancy Test

From a client machine:

- Confirm domain login still works
- Confirm `nslookup cyberrange.local` works
- Confirm access to domain resources works

Do not do a destructive outage test unless your team is ready for it, but at minimum verify the second controller is healthy and visible

---

# Part 2 — Build the Internal Web Server

# Purpose

The Internal Web Server provides a realistic enterprise service inside the Target Environment. It becomes a legitimate server to access, monitor, defend, and potentially attack later.

---

## Step 16 — Create the VM

In Proxmox:

- Create a new Windows Server 2022 VM or use the intended server OS from your topology
- Name it:

`Web-Server` or your chosen internal web server name

- Attach NIC to the Target network
- Start the VM

---

## Step 17 — Complete OS Installation and Drivers

If Windows setup appears:

- Complete installation
- Load VirtIO storage driver if necessary
- Install VirtIO guest tools
- Reboot

Confirm the NIC works before continuing

---

## Step 18 — Rename the Server

Rename the machine to the intended hostname

Restart after renaming

---

## Step 19 — Configure Static IP

Assign a static IP in the Target subnet

Use:

- Unused `10.20.20.x` address
- Subnet mask `255.255.255.0`
- Gateway `10.20.20.1`
- DNS `10.20.20.10`

---

## Step 20 — Verify Connectivity

Test:

- Ping Domain Controller
- Ping File Server
- `nslookup cyberrange.local`

Do not continue until connectivity is correct

---

## Step 21 — Join the Domain

Join the server to:

`cyberrange.local`

Restart after the join completes

---

## Step 22 — Verify Domain Join

After reboot:

- Log in with domain credentials
- Confirm the machine appears in Active Directory
- Move it to the correct server OU if needed

---

## Step 23 — Install the Web Server Role

Open Server Manager

Install:

`Web Server (IIS)`

Proceed through the Add Roles and Features wizard

Accept default required features

Finish installation

---

## Step 24 — Verify IIS Is Running

Open a browser on the server itself and go to:

`http://localhost`

You should see the default IIS page

If it does not load:
- Confirm IIS installed successfully
- Confirm service is running

---

## Step 25 — Create a Simple Internal Web Page

Navigate to:

`C:\inetpub\wwwroot`

Edit or replace the default page with a simple internal page

Example content:
- Company intranet
- Internal portal placeholder
- Basic HTML page

The point here is to have a real internal web service available

---

## Step 26 — Test the Site from Another Machine

From a domain-joined client:

- Open a browser
- Visit the web server by IP
- If DNS entry exists later, test by name as well

Confirm the internal site loads from another system

---

# Part 3 — Build the Windows Log Server

# Purpose

The Windows Log Server provides a dedicated system for centralized Windows event collection preparation. Even if full logging integration happens later, this system should be built now as part of completing the Target environment.

---

## Step 27 — Create the VM

In Proxmox:

- Create a new Windows Server 2022 VM
- Name it:

`Windows-Log-Server`

- Attach NIC to the Target network
- Start the VM

---

## Step 28 — Complete OS Installation and Drivers

If installation is required:

- Complete Windows installation
- Load VirtIO drivers if necessary
- Install guest tools
- Reboot

---

## Step 29 — Rename the Server

Rename the system to:

`Windows-Log-Server`

Restart after renaming

---

## Step 30 — Configure Static IP

Set:

- An unused `10.20.20.x` address
- Subnet mask `255.255.255.0`
- Gateway `10.20.20.1`
- DNS `10.20.20.10`

---

## Step 31 — Verify Connectivity

Test:

- Ping Domain Controller
- Ping File Server
- `nslookup cyberrange.local`

---

## Step 32 — Join the Domain

Join:

`cyberrange.local`

Restart after join

---

## Step 33 — Verify AD Placement

- Confirm the machine object appears in Active Directory
- Move it to the correct OU if needed

---

## Step 34 — Prepare Windows Event Collection

Log into the server with administrative rights

Open an elevated Command Prompt or PowerShell

Run:

`wecutil qc`

This initializes Windows Event Collector

If prompted, confirm the setup

---

## Step 35 — Prepare WinRM

Run:

`winrm quickconfig`

Confirm any prompts

This prepares the system for remote event forwarding and management support

---

## Step 36 — Verify the Server Is Ready

At this stage, you are not necessarily forwarding logs yet, but the server should be prepared for later integration

Confirm:
- The server is domain joined
- Event Collector initialized
- WinRM configured
- No major network issues exist

---

# Part 4 — Build the IT Admin Workstation

# Purpose

The IT Admin Workstation is the management workstation used to administer the enterprise environment without always working directly from the servers.

---

## Step 37 — Create the VM

In Proxmox:

- Create or clone a Windows 11 VM from the correct template
- Name it:

`IT-Admin-Workstation`

- Attach NIC to the Target network
- Start the VM

---

## Step 38 — Complete Windows Installation and Drivers

If Windows setup appears:

- Complete the installation
- Install VirtIO drivers
- Reboot if needed

---

## Step 39 — Rename the Workstation

Rename the system to:

`IT-Admin-Workstation`

Restart after renaming

---

## Step 40 — Configure Static or Planned IP Address

Depending on your addressing approach, assign the correct workstation IP in the Target network

Use:
- Valid `10.20.20.x`
- Gateway `10.20.20.1`
- DNS `10.20.20.10`

---

## Step 41 — Verify Connectivity

Test:
- Ping Domain Controller
- `nslookup cyberrange.local`

---

## Step 42 — Join the Domain

Join the workstation to:

`cyberrange.local`

Restart after the join

---

## Step 43 — Verify Domain Login

After reboot:

- Log in using the IT administrative account
- Confirm domain authentication works

---

## Step 44 — Install Administrative Tools

Open PowerShell as Administrator and install RSAT tools

Use the Windows capability install method already used in your project if applicable

Then verify you can launch:
- Active Directory Users and Computers
- DNS tools
- Group Policy tools if available

This system should become your normal management workstation

---

# Part 5 — Build the Incident Response Workstation

# Purpose

The Incident Response Workstation provides a non-server analysis system for defensive investigation and response tasks.

---

## Step 45 — Create the VM

In Proxmox:

- Create or clone an Ubuntu Desktop VM from the correct template
- Name it:

`IR-Workstation`

- Attach NIC to the Target network
- Start the VM

---

## Step 46 — Complete Ubuntu Setup

Complete the normal Ubuntu first-run or installation process

Set:
- Username
- Password
- Hostname if prompted

---

## Step 47 — Configure Networking

Assign the intended IP configuration for the workstation

Ensure:
- It is on the Target subnet
- It can reach the Domain Controller
- DNS resolution works if required for your use case

---

## Step 48 — Update the System

Open Terminal and run:

`sudo apt update`
`sudo apt upgrade -y`

This ensures the workstation starts from a current package state

---

## Step 49 — Install Basic IR / Network Tools

Install common tools needed for analysis

Examples already aligned with this build phase:
- `wireshark`
- `tcpdump`
- `net-tools`
- `curl`
- `git`

Install them using apt

---

## Step 50 — Verify Basic Functionality

Confirm:
- The system has network connectivity
- Terminal tools run correctly
- You can reach key internal systems by IP

This workstation does not need to be overbuilt yet. It just needs to be operational and ready for later use

---

# Part 6 — Build the Vulnerable Training Server

# Purpose

The Vulnerable Training Server provides intentional attack surface inside the Target environment for controlled offensive and defensive exercises.

---

## Step 51 — Create the VM

In Proxmox:

- Create or clone the intended Linux server VM
- Name it:

`Vuln-Training-Server`

- Attach NIC to the Target network
- Start the VM

---

## Step 52 — Complete OS Setup

Complete the normal Linux installation or first boot setup

Set:
- Hostname
- Username
- Password

---

## Step 53 — Configure Networking

Assign the correct IP settings for the Target environment

Confirm:
- IP connectivity works
- Gateway works
- Internal systems are reachable

---

## Step 54 — Update the System

Run:

`sudo apt update`
`sudo apt upgrade -y`

---

## Step 55 — Install Container Support or Required Platform

Because this machine is intended to host vulnerable applications, prepare the platform it needs

If using Docker-based deployment:

- Install Docker
- Enable Docker service
- Confirm Docker runs correctly

---

## Step 56 — Deploy the Vulnerable Application

Install the intended vulnerable application according to your topology plan

Examples that fit the project:
- DVWA
- Juice Shop

Deploy only the application you are actually using in your build documentation

---

## Step 57 — Verify Local Service Availability

On the server itself, confirm the service is listening on the intended port

---

## Step 58 — Verify Access from Another Machine

From a client machine:
- Open a browser
- Connect to the vulnerable application by IP and port

Confirm the site loads

This is the main proof that the vulnerable target is ready for later attack scenarios

---

# Part 7 — Build the Blue Team Analysis Workstation (Kali Purple)

# Purpose

The Blue Team Analysis Workstation provides a dedicated analyst box for security investigation and blue team activity.

---

## Step 59 — Create the VM

In Proxmox:

- Clone or create the Kali Purple VM from the correct template
- Name it:

`Kali-Purple` or your intended analyst hostname

- Attach NIC to the Target network if that is what your topology uses
- Start the VM

---

## Step 60 — Complete First Boot Setup

Complete Kali first boot setup if needed

Set:
- Username
- Password
- Hostname

---

## Step 61 — Configure Networking

Assign the correct IP settings for the machine

Confirm:
- It is on the intended network
- It can reach internal systems needed for analysis

---

## Step 62 — Update the System

Run:

`sudo apt update`
`sudo apt upgrade -y`

---

## Step 63 — Verify Blue Team Tool Availability

Confirm that core tools expected on Kali Purple are available and functioning

Examples include:
- packet analysis tools
- scanning tools
- system utilities

Do not over-customize yet unless your project specifically requires it at this phase

---

## Step 64 — Verify Internal Reachability

Test reachability to:
- Domain Controller
- File Server
- Web Server
- Vulnerable Training Server

This confirms the workstation is usable as an analyst platform inside the range

---

# Part 8 — Final Validation of the Completed Target Environment

# Purpose

This is the final full-environment validation step to confirm that the entire Target environment is complete and stable before moving on to the SOC / Detection build.

---

## Step 65 — Validate All Core Systems Exist and Boot Properly

Confirm all Target systems power on successfully and remain stable:

- Primary Domain Server
- Backup Domain Server
- File Server
- Internal Web Server
- Windows Log Server
- IT Admin Workstation
- Incident Response Workstation
- Vulnerable Training Server
- Kali Purple
- All Windows 10 clients
- All Windows 11 clients

---

## Step 66 — Validate Domain Services

From multiple Windows systems, confirm:

- Domain login works
- DNS resolves correctly
- Group Policy still applies
- File services still work

---

## Step 67 — Validate Inter-System Reachability

Confirm the right systems can reach the right internal services

Examples:
- Clients can reach File Server
- Clients can reach Internal Web Server
- IT Admin Workstation can manage domain systems
- Vulnerable app is reachable
- Log Server is reachable

---

## Step 68 — Validate AD Visibility

In Active Directory, confirm the newly added Windows systems appear correctly and are placed in the correct OUs as needed

---

## Step 69 — Validate Web and Vulnerable Services

Confirm:
- Internal web page loads
- Vulnerable app loads
- No obvious service startup failures exist

---

## Step 70 — Validate Management Systems

Confirm:
- IT Admin Workstation can be used for administration
- IR Workstation has tools installed and network access
- Kali Purple is usable for analysis

---

## Step 71 — Record Final Completion State

At the end of Phase 5, the Target Environment should now represent a completed enterprise-style environment that includes:

- identity infrastructure
- file services
- multiple endpoints
- web services
- admin workstations
- analyst workstations
- log collection preparation
- vulnerable services

This is the environment you will then monitor in the next phase

---

# Expected Results

By the end of Phase 05:

- All remaining Target VMs are built
- All Windows systems are domain joined where appropriate
- All Linux systems are network-functional
- Core enterprise services are present
- Internal web services are reachable
- Vulnerable services are reachable
- Administrative and analyst workstations are usable
- The Target environment is fully complete

---

# Common Mistakes to Avoid

- Building machines in random order
- Forgetting to install VirtIO drivers on Windows guests
- Using incorrect DNS on domain-joined systems
- Not renaming systems before joining the domain
- Skipping reboot steps after rename or domain join
- Forgetting to verify service availability from another machine
- Assuming a machine is complete without validating connectivity

---

# Phase Completion Criteria

Phase 05 is complete when:

- Backup Domain Server is operational and healthy
- Internal Web Server is operational
- Windows Log Server is prepared
- IT Admin Workstation is operational
- Incident Response Workstation is operational
- Vulnerable Training Server is operational
- Blue Team Analysis Workstation is operational
- Full Target environment validation is successful

---

# Transition to the Next Phase

After this phase is complete, the next phase is:

SOC / Detection Environment Setup

That phase will add visibility, monitoring, detection, and analysis on top of the now fully completed Target environment.

---

# Summary

Phase 05 completes the Target environment by adding the remaining enterprise systems, admin platforms, analyst platforms, and vulnerable services required for a realistic cyber range.

This phase is the final infrastructure expansion step before SOC integration begins.
