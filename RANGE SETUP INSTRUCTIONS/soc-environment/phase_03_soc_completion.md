# Marist SOC Cyber Range
# Lab Build Guide — Phase 03: SOC Environment Completion, Log Integration, and Cross-Environment Visibility

---

## Status

✅ NEARLY COMPLETE

The SOC / Detection Environment has been built to an operational state and is actively receiving telemetry from the Target Environment. At this stage, the major SOC systems are deployed, routing and segmentation are in place, Linux syslog forwarding is working, OPNsense firewall telemetry is working, and Elastic Agent has been installed on Target Environment machines and assigned to the Fleet policy.

The remaining unresolved items at the time of this documentation are:

- persistent Security Onion time / NTP reset issue
- persistent firewall / iptables reset issue affecting required Elastic / Fleet / Kibana ports:
  - `8220`
  - `8443`
  - `9200`

These are stability issues, not full build blockers. The SOC environment itself is otherwise operational and functionally built.

# Phase Overview

Phase 03 focused on completing the remaining SOC / Detection Environment systems and establishing practical log and telemetry flow from the Target Environment into Security Onion.

This phase documents the systems and integrations that were completed and validated during this stage of the build:

- Adversary-Simulation (MITRE Caldera)
- Range-Orchestration
- Target Linux rsyslog forwarding to Security Onion
- Elastic Agent deployment to Target Environment systems
- Fleet policy creation and agent enrollment for the Target Environment

The purpose of this phase was to move the SOC environment beyond initial platform deployment and segmentation into a working monitoring environment. This included completing the remaining SOC infrastructure, configuring Linux systems in the Target Environment to forward logs, deploying Elastic Agent to Target systems, organizing those agents under a dedicated Fleet policy, and validating that Security Onion could receive telemetry from systems across the Target subnet.

> Important scope note: This guide documents the final successful build path for the SOC environment completion work that was actually accomplished. It includes the working deployment and integration steps that brought the SOC environment to an operational state. The remaining unresolved stability issues involving Security Onion time synchronization and recurring port / iptables resets are documented separately as known open issues and are not treated as incomplete build steps for this phase.

---

# Phase 03 Objectives

- Build and prepare the Adversary-Simulation server
- Build and prepare the Range-Orchestration server
- Configure Security Onion to accept Target Environment syslog traffic
- Configure rsyslog on Target Linux systems to forward logs to Security Onion
- Validate Linux log transport from the Target Environment into Security Onion
- Create a dedicated Fleet policy for Target Environment systems
- Deploy Elastic Agent to Target Environment machines
- Enroll Target systems into the `Target-Ennvironment-Policy`
- Validate that Security Onion is receiving firewall, Linux, and endpoint telemetry
- Complete the practical SOC-side integration between the Target and SOC environments

---

# Final Outcome

- Adversary-Simulation deployed and operational
- Range-Orchestration deployed and prepared
- Security Onion configured to accept syslog from the Target subnet
- Target Linux systems forwarding logs through rsyslog
- OPNsense firewall telemetry visible in Security Onion
- Elastic Agent installed on Target Environment systems
- Target agents enrolled into `Target-Ennvironment-Policy`
- SOC environment functioning as an operational monitoring space
- Remaining open issues limited to time synchronization persistence and recurring port / iptables resets affecting `8220`, `8443`, and `9200`

---

# Important Design Notes

## Security Onion as the Central Collection Platform

In this phase, Security Onion was used as the central collection and monitoring platform for the SOC environment.

This means:

- OPNsense forwards firewall telemetry to Security Onion
- Target Linux systems forward logs directly to Security Onion
- Target endpoints use Elastic Agent to send host telemetry into Security Onion through Fleet

The originally planned Linux Log Server was not used as part of the final active design for this phase because direct forwarding to Security Onion simplified the environment and reduced unnecessary complexity.

---

## Cross-Environment Monitoring Path

This phase represents the point where the SOC environment became operational across subnet boundaries.

The practical monitoring path established in this phase was:

- Target Environment systems generate logs and telemetry
- OPNsense permits the required paths
- Security Onion receives and manages the telemetry from the SOC subnet

This was the first phase where the SOC environment began functioning as a true monitoring layer for the enterprise systems built in the Target Environment.

---

## Remaining Stability Issues

Although this phase was operationally completed, two important stability issues remained open at the end of the build work documented here:

- Security Onion time / NTP behavior can reset and must be stabilized
- Required Elastic / Security Onion ports can stop working until firewall / iptables behavior is corrected again:
  - `8220`
  - `8443`
  - `9200`

These issues affect long-term reliability but do not change the fact that the systems and integrations in this phase were successfully built and validated.

---

# Purpose

This phase completes the practical build-out of the SOC / Detection Environment for the Marist SOC Cyber Range.

The purpose of this phase is to move the SOC from an initial standalone deployment into a working defensive environment that can:

- receive logs from the Target Environment
- monitor activity across segmented subnets
- host a SIEM / SOC platform
- support analyst access from dedicated SOC workstations
- enforce network segmentation between the Target and SOC environments
- support host-based telemetry through Elastic Agent
- support Linux log forwarding through rsyslog
- support future adversary simulation and orchestration activity

By the end of this phase, the SOC environment should function as the defensive monitoring side of the cyber range and provide the visibility needed for future scenario execution, investigation, and response.

---

# Environment Overview

The SOC / Detection Environment is the defensive side of the cyber range.

It is used to provide:

- centralized monitoring
- firewall logging
- host telemetry collection
- SOC analyst access
- future detection engineering
- future alert triage
- future incident investigation
- future adversary simulation and orchestration

This environment is separated from the Red Team and Target environments so the cyber range behaves like a real segmented enterprise design.

---

# SOC Network Design

## SOC / Detection Subnet

- Subnet: `10.20.30.0/24`
- Gateway: `10.20.30.1`

## Target Subnet

- Subnet: `10.20.20.0/24`
- Gateway: `10.20.20.1`

## Proxmox Bridge Mapping

- `vmbr2` → Target Environment
- `vmbr3` → SOC / Detection Environment

## Important Routing Design

The OPNsense firewall is the active segmentation device between the Target and SOC networks.

In this design:

- OPNsense LAN = Target side
- OPNsense WAN = SOC side

That means:

- LAN interface sits on `10.20.20.0/24`
- WAN interface sits on `10.20.30.0/24`

This is intentional for this cyber range design and was used successfully during build and validation.

---

# Systems Included in the SOC Environment

## Core SOC Infrastructure

- `Security-Onion` → `10.20.30.10`
- `Firewall-Segmentation` → `10.20.30.20`
- `Core-Network-Router` → `10.20.30.40`

## Detection / Simulation Systems

- `Adversary-Simulation` → `10.20.30.50`
- `Range-Orchestration` → `10.20.30.70`

## SOC Workstations

- `SOC-Admin-Workstation` → DHCP / reserved
- `SOC-Analyst-Workstation` → DHCP / reserved

---

# Important Design Notes

## 1. Security Onion is not domain joined

Security Onion uses:

- Primary DNS: `10.20.20.10`
- Secondary DNS: `10.20.20.11`

It also uses:

- DNS search domain: `cyberrange.local`

This does NOT mean Security Onion is joined to Active Directory.

Security Onion is used for:

- DNS resolution
- SOC platform access
- log ingestion
- monitoring

The SOC workstations are domain joined. Security Onion is not.

---

## 2. Time synchronization matters

All systems in the cyber range must remain closely time synchronized.

This is critical because time drift can cause:

- dashboard login failures
- broken correlation between logs
- inconsistent event timelines
- authentication problems

At the time of this documentation, a recurring time reset problem still exists on the Security Onion side and must be resolved for long-term stability.

---

## 3. Port stability matters

The following Security Onion / Elastic related ports are required to remain reachable when using Fleet and the web platform:

- `8220` → Fleet / Elastic Agent enrollment and management
- `8443` → Security Onion web / package access path used in this build
- `9200` → Elastic / backend access used during validation

At the time of this documentation, these ports sometimes stop working until firewall / iptables rules are corrected again. This is one of the remaining unresolved issues in the SOC build.

---

## 4. Linux Log Server was not used in the final active design

The original SOC IP plan included a Linux Log Server, but during the build it was determined that this was unnecessary for the current project state.

Instead, the final active design used:

- Target Linux systems → forward directly to Security Onion

This reduced complexity and simplified troubleshooting.

---

## 5. OPNsense is the active segmentation device

The Core-Network-Router exists and was built successfully, but it is reserved for future scenarios and is not the active production routing path for the current project.

OPNsense is the main system handling segmentation between:

- Target Environment
- SOC Environment

---

# Part 1 — Build Security Onion

## Step 1 — Download the correct Security Onion ISO

Use the Security Onion 2.4 ISO for this build.

The final successful build path used Security Onion 2.4 rather than Security Onion 3.0.

Reason:

- Security Onion 3.0 was avoided due to instability during deployment
- Security Onion 2.4 provided the stable working path for this cyber range

---

## Step 2 — Upload the ISO to Proxmox

In Proxmox:

- upload the Security Onion ISO to the proper storage location
- verify the ISO is visible and available for VM creation

---

## Step 3 — Create the Security Onion VM

In Proxmox:

- create a new VM
- name it:

`Security-Onion`

- attach the Security Onion ISO
- configure the VM with the project’s planned hardware allocation

Final working build values used:

- RAM: `24 GB`
- CPU: `8 cores`
- BIOS: `OVMF (UEFI)`
- Machine Type: `q35`
- Disk: `330 GB`
- SCSI: `VirtIO`

---

## Step 4 — Configure NICs for Security Onion

Attach two NICs to the Security Onion VM.

Use:

- `net0` → `vmbr3` → SOC management network
- `net1` → `vmbr2` → Target network visibility / monitoring side

This gives Security Onion:

- one management-facing interface in the SOC network
- one interface with visibility into the Target-side traffic design

---

## Step 5 — Install Security Onion

Boot the VM from the ISO and complete the normal Security Onion installation process.

During setup, configure the management interface with:

- IP Address: `10.20.30.10`
- Subnet Mask: `255.255.255.0`
- Gateway: `10.20.30.1`
- DNS1: `10.20.20.10`
- DNS2: `10.20.20.11`
- Domain / search domain: `cyberrange.local`

Verify interface mapping during installation:

- management NIC = SOC side
- monitoring NIC = Target side

In the final working build, the interface mapping was confirmed as:

- `ens18` → management
- `ens19` → monitoring

---

## Step 6 — Complete Security Onion initialization

Allow the installation to finish and complete the Security Onion setup process.

Once complete, validate that the platform loads from a SOC workstation at:

`https://10.20.30.10`

Only access the dashboard from permitted SOC systems.

---

## Step 7 — Validate Security Onion health

After installation, confirm:

- the system boots normally
- the IP address is correct
- DNS resolution works
- the dashboard loads
- the main Security Onion services are running

During later troubleshooting, the following Security Onion-side checks were used successfully:

- `sudo so-status`
- `sudo so-status | grep fleet`
- `sudo ss -tulmp | grep -E "8220|8443|9200"`

These checks confirmed that the Security Onion services and listeners were healthy when the platform was functioning correctly.

---

# Part 2 — Build the SOC Workstations

## Step 8 — Build the SOC Admin Workstation

Create or clone a Windows workstation VM for the SOC administrator.

Use a Windows template already prepared in the environment.

Name it:

`SOC-Admin-Workstation`

Attach the NIC to:

`vmbr3`

This places it on the SOC network.

---

## Step 9 — Build the SOC Analyst Workstation

Create or clone a second Windows workstation VM for analyst use.

Name it:

`SOC-Analyst-Workstation`

Attach the NIC to:

`vmbr3`

This also places it on the SOC network.

---

## Step 10 — Configure DNS on both SOC workstations

For both SOC workstations, configure DNS to use the Target domain controllers:

- Primary DNS: `10.20.20.10`
- Secondary DNS: `10.20.20.11`

This is required because:

- the workstations are domain joined
- the Active Directory environment exists in the Target subnet
- the SOC workstations must resolve `cyberrange.local`

---

## Step 11 — Join both SOC workstations to the domain

Join both systems to:

`cyberrange.local`

Restart each system after the join completes.

Validate that domain login works after reboot.

---

## Step 12 — Create SOC-specific AD structure

On the Domain Controller, create SOC-specific organizational units and groups.

OUs created for the SOC side included:

- `SOC-WORKSTATIONS`
- `SOC-DEPARTMENT`
  - `SOC-Admin`
  - `SOC-Analyst`

Security groups created included:

- `SOC-Admins`
- `SOC-Analysts`

SOC users created included:

- `socadmin`
- `socanalyst`

Add the users to the correct SOC groups.

---

## Step 13 — Restrict local logon and RDP to SOC roles

Use Group Policy to restrict access on the SOC workstations.

Allow log on locally to:

- `Administrators`
- `SOC-Admins`
- `SOC-Analysts`

Allow RDP to:

- `Administrators`
- `SOC-Admins`
- `SOC-Analysts`

This prevents normal non-SOC domain users from signing into the dedicated SOC machines.

---

## Step 14 — Create dashboard accounts in Security Onion

Create Security Onion dashboard accounts for the SOC users.

The final working SOC dashboard accounts used:

- `socadmin@cyberrange.local`
- `socanalyst@cyberrange.local`

Password used in the lab standard build:

`Cyberrange2026`

These are Security Onion application accounts, not domain-joined Security Onion identities.

---

## Step 15 — Validate dashboard access from the SOC workstations

From the SOC-Admin-Workstation and SOC-Analyst-Workstation:

- open the Security Onion dashboard
- verify the page loads
- verify the SOC credentials work

A major issue encountered during this phase was time mismatch. Dashboard access only worked correctly once the time on Security Onion and the Windows systems was aligned closely enough.

---

# Part 3 — Build the Firewall Segmentation Server

## Step 16 — Upload the OPNsense ISO

Upload the OPNsense ISO to Proxmox.

The ISO used for this build was:

`OPNsense-25.1-dvd-amd64.iso`

---

## Step 17 — Create the OPNsense VM

In Proxmox:

- create a new VM
- name it:

`Firewall-Segmentation`

- attach the OPNsense ISO
- assign hardware resources based on the project’s design

Working build values used were approximately:

- RAM: `8 GB`
- CPU: `4 cores`
- Machine Type: `q35`
- Disk: `65 GB`
- SCSI: `VirtIO`

---

## Step 18 — Attach OPNsense NICs

Configure two NICs:

- `net0` → `vmbr3` → SOC network
- `net1` → `vmbr2` → Target network

Disable the Proxmox firewall on both NICs so OPNsense itself controls packet filtering.

---

## Step 19 — Install OPNsense

Boot from the ISO and complete the OPNsense installation.

Reboot into the OPNsense console when complete.

---

## Step 20 — Assign interfaces in OPNsense

From the OPNsense console, assign interfaces as follows:

- WAN → SOC side
- LAN → Target side

In the final working build:

- WAN = `vtnet0`
- LAN = `vtnet1`

---

## Step 21 — Assign interface IPs

Configure the OPNsense interfaces with the following addresses.

### WAN / SOC side

- IP Address: `10.20.30.20`
- Prefix: `/24`

### LAN / Target side

- IP Address: `10.20.20.1`
- Prefix: `/24`

This made OPNsense the active gateway and segmentation point between the Target and SOC networks.

---

## Step 22 — Access the OPNsense web GUI

From a SOC workstation, browse to:

`https://10.20.30.20`

Sign in with the OPNsense administrator credentials and complete normal first-access setup if needed.

---

## Step 23 — Restrict firewall GUI access to SOC systems only

Create OPNsense rules so that only SOC systems can reach the firewall GUI.

### WAN rule

Allow:

- Source: `10.20.30.0/24`
- Destination: WAN address
- Port: `443`

### Block non-SOC access

Block any unwanted access to the WAN address on `443`.

### LAN rule

Block:

- Source: `10.20.20.0/24`
- Destination: WAN address
- Port: `443`

Enable logging on the block rule so attempted access is recorded.

This ensures:

- SOC workstations can manage the firewall
- Target systems cannot access firewall management

---

## Step 24 — Forward OPNsense logs to Security Onion

In OPNsense:

Go to:

`System → Settings → Logging → Remote`

Enable remote logging and configure:

- Transport: `UDP`
- Remote IP: `10.20.30.10`
- Port: `514`

On Security Onion, prepare the syslog configuration so logs from the firewall are accepted.

Synchronize the changes.

---

## Step 25 — Validate OPNsense logs inside Security Onion

Generate test traffic from a Target system by trying to access:

`https://10.20.30.20`

Then validate:

- the deny appears in OPNsense live logs
- the forwarded firewall telemetry appears in Security Onion Hunt

Use searches such as:

`filterlog`

This confirmed that OPNsense logging into Security Onion was working.

---

# Part 4 — Build the Core Network Router

## Step 26 — Create the Core-Network-Router VM

Create an Ubuntu Server VM for future routing scenarios.

Name it:

`Core-Network-Router`

Attach the primary NIC to the SOC network.

---

## Step 27 — Configure the Core-Network-Router networking

Assign a static address:

- IP Address: `10.20.30.40`
- Prefix: `/24`

A second NIC was added for future routing use, but the router was intentionally not left in the active production path for the current project.

---

## Step 28 — Clean the routing configuration

Validate that the Core-Network-Router is reachable, but make sure it is not interfering with the OPNsense routing design.

The design decision for this build was:

- OPNsense remains the active segmentation device
- Core-Network-Router remains staged for future scenarios only

---

## Step 29 — Validate final Core-Network-Router state

Confirm:

- it powers on
- it is reachable
- it has the correct static IP
- it is not taking over the active routing role

This machine was successfully built and stabilized, then intentionally left reserved for future expansion.

---

# Part 5 — Configure Security Onion Syslog Acceptance for Target Linux Hosts

## Step 30 — Review the original Security Onion syslog allowlist

Initially, the Security Onion syslog host allowlist only permitted the firewall IP.

That meant only:

- `10.20.30.20`

was allowed to send syslog.

This was not enough for the Target Linux machines.

---

## Step 31 — Expand the allowed syslog source range

Update the Security Onion syslog configuration so the following are allowed:

- `10.20.20.0/24`
- `10.20.30.20`

This allows:

- all Linux systems in the Target subnet to send syslog
- the firewall to continue sending syslog

---

## Step 32 — Confirm Target Linux systems route through OPNsense

On the Linux systems in the Target network, verify the routing table with:

`ip route`

The key Target Linux systems checked during the build included:

- `IR-Workstation`
- `Kali Purple`
- `Vuln-Training-Server`
- Network traffic generator system

Each system needed to show a default route using:

`10.20.20.1`

This confirmed that Target Linux traffic was correctly routing through OPNsense.

---

# Part 6 — Configure rsyslog on the Target Linux Machines

## Step 33 — Install rsyslog where needed

On each Linux machine in the Target Environment, ensure `rsyslog` is installed and running.

Important note from the build:

- some Linux systems already had rsyslog
- Kali Purple did not initially have rsyslog present
- Kali Purple later had rsyslog installed successfully

This is important because not every Linux image will be identical.

---

## Step 34 — Create the Security Onion forwarding config file

On each Linux machine, create:

`/etc/rsyslog.d/99-securityonion.conf`

Add the following line:

`*.* @10.20.30.10:514`

This forwards all syslog messages over UDP to Security Onion.

---

## Step 35 — Restart and verify rsyslog

Run:

`sudo systemctl restart rsyslog`

Then verify:

`systemctl status rsyslog`

If the service is missing, install rsyslog first, then enable and restart it.

This exact issue was encountered on Kali Purple during the build.

---

## Step 36 — Generate test log traffic

Use the logger command on each Linux system to generate a test event.

Example pattern used during validation:

`logger "test message"`

This creates a log event that should be forwarded immediately.

---

## Step 37 — Validate transport with tcpdump

Use `tcpdump` to prove syslog transport is working.

Examples used during troubleshooting included:

- run `tcpdump -i any port 514` on the Linux machine
- run `tcpdump -i any port 514` on Security Onion

This allowed confirmation that:

- packets left the Linux machine
- packets arrived at Security Onion

During validation, Security Onion was observed receiving traffic types such as:

- `authpriv.info`
- `cron.info`
- `user.notice`

---

## Step 38 — Understand the ingestion result

A key lesson from the build was that successful syslog transport does not automatically mean the logs will appear in a useful searchable format in Hunt.

What was proven:

- raw syslog packets were reaching Security Onion
- transport worked
- the remaining limitation was ingestion / parsing / indexing behavior for generic syslog

Even so, the Linux forwarding layer itself was considered successfully built.

---

# Part 7 — Build the Adversary Simulation Server

## Step 39 — Create the Adversary-Simulation VM

Create an Ubuntu-based VM in the SOC subnet.

Name it:

`Adversary-Simulation`

Assign:

- IP Address: `10.20.30.50`

Attach the NIC to the SOC bridge.

---

## Step 40 — Prepare the system

Update the system and install required dependencies for MITRE Caldera.

Typical requirements included:

- Python 3
- Git
- Python virtual environment support
- required Python packages

---

## Step 41 — Install MITRE Caldera

Clone the Caldera repository.

Create and activate a virtual environment.

Start the platform with:

`python3 server.py --insecure`

The `--insecure` flag was required in the working lab setup to get the UI functioning during this phase.

---

## Step 42 — Validate Caldera access

Access the Caldera UI at:

`http://10.20.30.50:8888`

Confirm the UI loads.

During validation, the platform showed:

- Caldera version loaded
- abilities and adversaries loaded
- server listening on `0.0.0.0:8888`

Some warnings appeared, such as:

- insecure mode warning
- GitHub token warning
- payload / plugin warnings
- missing ability reference warnings

These were treated as non-blocking for infrastructure completion.

The platform was considered operational.

---

# Part 8 — Build the Range Orchestration Server

## Step 43 — Create the Range-Orchestration VM

Create a server in the SOC subnet.

Name it:

`Range-Orchestration`

Assign:

- IP Address: `10.20.30.70`

Attach the NIC to the SOC network.

---

## Step 44 — Prepare the system

Update the server and install the core tooling needed for orchestration and future automation.

Packages and tooling prepared included:

- `git`
- `curl`
- `wget`
- `unzip`
- `python3`
- `python3-pip`
- `python3-venv`
- `ansible`

---

## Step 45 — Create the working directory structure

Create directories for future orchestration work, such as:

- `scenarios`
- `scripts`
- `logs`
- `docs`

This server was successfully brought to a prepared operational state for future scenario control and automation.

---

# Part 9 — Prepare Fleet for Target Endpoint Telemetry

## Step 46 — Identify the correct Fleet policy

Inside Security Onion Fleet, review the available policies.

The correct endpoint policy for Target Environment hosts was:

`endpoints-initial`

Important:

Do NOT use the `so-grid-nodes_*` policies for standard Target endpoints.

Those are intended for Security Onion infrastructure nodes, not normal monitored systems.

---

## Step 47 — Create the dedicated Target Environment policy

A Fleet policy was created for this cyber range build named:

`Target-Ennvironment-Policy`

This became the policy where the Target Environment agents live.

All Target endpoints intended for host-based telemetry are assigned into this policy.

---

## Step 48 — Prepare access to the required Security Onion ports

Elastic Agent enrollment and package access required the following ports to function between the Target subnet and Security Onion:

- `8220`
- `8443`
- `9200`

These ports were later validated as listening on Security Onion when the services were healthy.

---

# Part 10 — Create the OPNsense Port Alias for Security Onion Access

## Step 49 — Create the alias in OPNsense

In OPNsense, create a port alias named:

`SEC_ONION_PORTS`

Type:

`Port(s)`

Add:

- `8220`
- `8443`
- `9200`

Description example:

`Security Onion Elastic / Fleet ports`

This alias simplifies later rule creation and reduces mistakes.

---

## Step 50 — Create the required allow rule

Create the firewall rule that allows the Target subnet to reach Security Onion on the necessary ports.

Use logic equivalent to:

- Action: Pass
- Interface: the interface matching the actual packet path in your active design
- Direction: in
- Protocol: TCP
- Source: `10.20.20.0/24`
- Destination: `10.20.30.10`
- Destination Port: `SEC_ONION_PORTS`

Important build lesson:

During troubleshooting, interface placement and rule matching had to be checked carefully because the environment design uses OPNsense between the Target and SOC networks and packet path matters. The final working state required making sure the rule matched the real traffic path and that the alias / destination host were entered correctly.

---

## Step 51 — Validate target-to-Security Onion connectivity

From a Target endpoint, test the ports using PowerShell or other connectivity tools.

Examples used during validation:

- `Test-NetConnection 10.20.30.10 -Port 8220`
- `Test-NetConnection 10.20.30.10 -Port 8443`
- `Test-NetConnection 10.20.30.10 -Port 9200`

These checks were important because they separated:

- routing problems
- service problems
- firewall problems

The final working state required these ports to remain reachable, though port persistence is still one of the current unresolved issues.

---

# Part 11 — Install Elastic Agent on the Target Machines

## Step 52 — Start with one endpoint first

During the build, the first install path started with a single Windows endpoint so the workflow could be validated before wider rollout.

After that workflow was proven, the installation expanded to the rest of the Target machines.

This is the recommended build approach because it reduces troubleshooting scope.

---

## Step 53 — Obtain the Elastic Agent installer

Use the Security Onion Downloads page and the enrollment command generated by Fleet.

Important lesson from the build:

Make sure you are using the actual installer package or the proper Fleet-provided install command, not a `.url` shortcut or a placeholder file.

---

## Step 54 — Install the agent on Windows systems

Run the Fleet-generated Windows installation command on each Windows Target machine from an elevated shell.

During the project build, this was first tested on a Windows 10 target system and later expanded.

Validate after installation that the endpoint appears in Fleet and is assigned to:

`Target-Ennvironment-Policy`

---

## Step 55 — Install the agent on Linux systems

Run the Fleet-generated Linux installation command on each Linux machine in the Target Environment.

This was completed for the Linux hosts in the environment as part of the final build progression.

Validate after installation that each Linux host appears in Fleet under:

`Target-Ennvironment-Policy`

---

## Step 56 — Confirm agent status across the Target Environment

At the current project state, Elastic Agent has been installed across the Target Environment systems and the hosts live inside the Fleet policy named:

`Target-Ennvironment-Policy`

Confirm from Fleet that the agents show expected health and are checking in.

---

# Part 12 — Validate SOC Telemetry Sources

## Step 57 — Validate Security Onion dashboard access

From the SOC workstations, confirm the dashboard loads and SOC accounts can sign in.

If login fails unexpectedly, verify time synchronization first.

---

## Step 58 — Validate OPNsense log ingestion

Search in Security Onion Hunt for firewall data such as:

`filterlog`

Confirm that OPNsense events are visible.

---

## Step 59 — Validate Linux syslog forwarding

Generate a test log from a Linux host with `logger` and confirm transport reaches Security Onion.

Use `tcpdump` if needed for proof.

---

## Step 60 — Validate Elastic Agent enrollment

In Fleet, confirm that the Target systems show up in the policy:

`Target-Ennvironment-Policy`

This confirms host-based telemetry enrollment.

---

## Step 61 — Validate cross-environment routing behavior

Confirm the following general network behavior:

- SOC systems can access SOC resources they are supposed to manage
- Target systems can reach only the allowed Security Onion services
- Target systems cannot reach the firewall GUI
- logging and monitoring traffic follows the allowed paths
- segmentation remains intact

---

# Part 13 — Current Known Open Issues

## Step 62 — Document the recurring time reset problem

At this stage of the project, Security Onion still has a recurring time / NTP related issue where the time can reset or drift.

This must still be corrected because it can affect:

- dashboard authentication
- event correlation
- investigation accuracy

---

## Step 63 — Document the recurring port reset problem

At this stage of the project, the required Security Onion / Elastic related ports can stop working until firewall / iptables behavior is corrected again.

The impacted ports are:

- `8220`
- `8443`
- `9200`

This must be stabilized so that:

- Fleet remains consistently reachable
- log ingestion remains reliable
- the environment remains ready for repeated student use without manual intervention

---

# Part 14 — Final Completion State for This Phase

## Step 64 — Confirm what is complete

At this point, the following are complete:

- Security Onion is deployed
- SOC Admin and SOC Analyst workstations are deployed
- both SOC workstations are domain joined
- SOC-specific users, groups, and OUs were created
- Security Onion dashboard access works from SOC systems
- OPNsense is deployed and functioning as the segmentation firewall
- OPNsense logging is forwarded into Security Onion
- Core-Network-Router is built and staged for future use
- Adversary-Simulation server is operational
- Range-Orchestration server is operational
- rsyslog is installed and functioning on the Target Linux hosts
- Elastic Agent is installed on the Target machines
- Target agents are managed through the Fleet policy:
  - `Target-Ennvironment-Policy`

---

## Step 65 — Confirm what still needs stabilization

The following items remain open:

- permanent fix for Security Onion time / NTP reset behavior
- permanent fix for the recurring firewall / iptables reset affecting:
  - `8220`
  - `8443`
  - `9200`

These are the final remaining stabilization tasks for the SOC environment at the time of this documentation.

---

# Expected Results

By the completion of this phase, the SOC environment should provide:

- a functioning SIEM / SOC platform
- firewall telemetry
- Linux log forwarding
- endpoint telemetry through Elastic Agent
- analyst workstations
- segmentation between Target and SOC
- prepared adversary simulation and orchestration systems
- a repeatable base for future blue team exercises

---

# Common Mistakes to Avoid

- using the wrong Security Onion version during deployment
- domain joining Security Onion
- mixing up the SOC and Target interfaces on OPNsense
- forgetting that OPNsense LAN is the Target side and WAN is the SOC side in this design
- forgetting to allow Target access to the required Security Onion service ports
- using the wrong Fleet policy for endpoints
- confusing a `.url` shortcut with the actual installer
- assuming syslog transport automatically means searchable parsed events in Hunt
- forgetting to install rsyslog on Linux systems that do not already have it
- allowing the Core-Network-Router to interfere with the active OPNsense routing path
- ignoring time synchronization problems

---

# Phase Completion Criteria

This phase is considered operationally complete when all of the following are true:

- Security Onion is installed and reachable
- SOC workstations are built and domain joined
- OPNsense is deployed with correct interface mapping and segmentation rules
- firewall logs are visible in Security Onion
- Core-Network-Router is built and non-interfering
- Adversary-Simulation is built and reachable
- Range-Orchestration is built and prepared
- Target Linux systems can forward logs
- Elastic Agent is installed across the Target systems
- the Fleet policy `Target-Ennvironment-Policy` contains the enrolled Target machines

For full long-term production readiness in the lab, the remaining required fixes are:

- persistent time synchronization stability
- persistent port / iptables rule stability for `8220`, `8443`, and `9200`

---

# Transition to the Next Phase

After these final stability issues are fixed, the next work should focus on:

- final detection validation
- attack-to-detection scenario execution
- rule development
- alert tuning
- investigation workflows
- student blue team operating procedures
- orchestration-assisted scenario delivery

---

# Summary

Phase 03 completes the functional build of the SOC / Detection Environment for the Marist SOC Cyber Range.

This phase established:

- Security Onion as the central monitoring platform
- dedicated SOC workstations for administration and analysis
- OPNsense as the segmentation and logging firewall
- future-ready supporting infrastructure through the Core-Network-Router, Adversary-Simulation server, and Range-Orchestration server
- Linux log forwarding through rsyslog
- endpoint telemetry through Elastic Agent and Fleet
- real cross-environment visibility between the Target and SOC environments

The SOC environment is now essentially built and operational, with the remaining work focused on stabilizing time synchronization and the recurring port / iptables issue so the platform remains consistently ready for repeated use in cyber range exercises.
