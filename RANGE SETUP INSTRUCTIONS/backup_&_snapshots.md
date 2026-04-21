# Marist SOC Cyber Range
# Backup and Snapshot Procedure for All Cyber Range Machines

---

## Purpose

This document explains the exact step-by-step process used to create backups and snapshots for every machine in the Marist Cyber Range.

The goal of this process is to protect the environment before major changes, scenario execution, adversary simulation, detection testing, log pipeline changes, and infrastructure modifications.

Creating both snapshots and backups is important because they serve different purposes:

- **Snapshots** allow very fast rollback of a VM to a recent state
- **Backups** provide a restorable copy of the VM if a larger failure occurs

For this project, every machine in the cyber range should be protected using this process before major changes are made.

---

## What Must Be Protected

This procedure should be performed for all machines across all cyber range environments:

### Red Team Environment
- Student-Attacker-01
- Student-Attacker-02
- Student-Attacker-03
- Student-Attacker-04
- Student-Attacker-05
- Student-Attacker-06
- Instructor-Attacker
- Red-Team-Jump-Server

### Target Environment
- Primary-Domain-Server
- Backup-Domain-Server
- File-Server
- Internal-Web-Server
- Windows-Log-Server
- Vuln-Training-Server
- Windows10-User-01
- Windows10-User-02
- Windows10-User-03
- Windows11-User-01
- Windows11-User-02
- Windows11-User-03
- IT-Admin-Workstation
- IR-Workstation
- Blue-Team-Analysis / Kali Purple
- any additional target systems such as the traffic generator if present in the final build

### SOC / Detection Environment
- Security-Onion
- Firewall-Segmentation
- Core-Network-Router
- Adversary-Simulation
- Range-Orchestration
- SOC-Admin-Workstation
- SOC-Analyst-Workstation

---

# Part 1 — Understand the Difference Between a Snapshot and a Backup

## Step 1 — Snapshot purpose

A snapshot is a point-in-time rollback state stored at the Proxmox VM level.

Use snapshots when:

- you are about to make configuration changes
- you are about to install tools or agents
- you are about to test detection logic
- you are about to run a scenario
- you may need to quickly revert the VM

Snapshots are useful for fast rollback, but they are not a replacement for a real backup.

---

## Step 2 — Backup purpose

A backup is a full saved copy of the VM stored in Proxmox backup storage.

Use backups when:

- you want recovery protection beyond a simple rollback
- you need to restore a deleted or broken VM
- you want to preserve a stable milestone
- you want to recover from major corruption or destructive scenario activity

Backups take longer than snapshots, but they provide stronger recovery capability.

---

## Step 3 — Best practice for this cyber range

Before major project work, use both:

1. create a **snapshot**
2. create a **backup**

This gives both:

- quick rollback
- full recovery protection

---

# Part 2 — Prepare Before Creating Snapshots and Backups

## Step 4 — Log into Proxmox

Open the Proxmox web interface and sign in to the `cyberrange` node.

Make sure you are working on the correct Proxmox host and storage.

---

## Step 5 — Confirm the VM list

In the left-hand Proxmox tree, review all VMs and confirm the machines that need protection.

Do not assume you remember every system from memory.

Check each environment and confirm that every machine is accounted for before continuing.

---

## Step 6 — Decide on the protection point

Before creating snapshots and backups, decide what milestone you are protecting.

Examples:

- before Security Onion configuration changes
- before Elastic Agent deployment
- before firewall rule changes
- before running Caldera
- before starting full red team scenarios
- before making detection engineering changes

This matters because the names and notes for snapshots and backups should clearly describe the protected state.

---

## Step 7 — Ensure VMs are in a stable state

Before protecting a VM:

- make sure the machine is powered on if you want a live-state snapshot
- make sure there are no incomplete installs running
- make sure no VM is in the middle of a reboot
- make sure no VM is frozen or locked
- make sure no disk-intensive process is halfway complete unless you intentionally want to capture that state

The cleaner the machine state, the cleaner the restore point.

---

# Part 3 — Create a Snapshot for a VM

## Step 8 — Select the VM in Proxmox

In the Proxmox left-side panel:

- click the VM name you want to protect

This opens the management view for that VM.

---

## Step 9 — Open the Snapshots tab

Inside that VM’s view:

- click the `Snapshots` tab

This is where Proxmox stores VM snapshots.

---

## Step 10 — Create the snapshot

Click:

`Take Snapshot`

A window will appear asking for snapshot details.

---

## Step 11 — Name the snapshot clearly

Use a consistent naming format that tells you exactly what state the machine was in.

Recommended format:

`pre-change-YYYY-MM-DD-description`

Examples:

- `pre-soc-testing-2026-04-20`
- `pre-elastic-agent-rollout-2026-04-20`
- `pre-caldera-scenario-2026-04-20`
- `stable-baseline-before-scenarios`

The name should make sense months later.

---

## Step 12 — Add a description

In the description or notes field, write exactly what the VM state represents.

Example:

- domain joined and validated
- Elastic Agent installed and healthy
- rsyslog configured and tested
- Security Onion reachable from SOC workstations
- firewall rules stable before scenario execution

This is very important because later you may have many snapshots and need to know which one is safe to restore.

---

## Step 13 — Decide whether to include RAM state

If Proxmox gives the option to include memory / RAM state:

- include RAM state if you want the VM restored exactly as it was running
- do not include RAM state if you only need the disk / configuration state

For general cyber range milestone protection, a normal snapshot without depending heavily on RAM state is usually easier to manage unless you specifically need an exact in-memory restore.

---

## Step 14 — Confirm snapshot creation

Click the button to create the snapshot.

Wait for Proxmox to finish.

Do not start other major actions on that VM while the snapshot is being created.

---

## Step 15 — Verify the snapshot exists

After creation completes:

- confirm the snapshot appears in the Snapshots tab
- confirm the name is correct
- confirm the description is correct

Do not move on until you verify it exists successfully.

---

# Part 4 — Repeat Snapshot Creation for Every VM

## Step 16 — Create a snapshot for each machine

Repeat Steps 8 through 15 for every VM in the cyber range.

This should include all:

- Red Team VMs
- Target VMs
- SOC VMs

Do not skip infrastructure systems.

Important systems that should absolutely be snapshotted before scenario work include:

- Primary-Domain-Server
- Backup-Domain-Server
- File-Server
- Windows-Log-Server
- Vuln-Training-Server
- all Windows clients
- Security-Onion
- Firewall-Segmentation
- Adversary-Simulation
- Range-Orchestration
- SOC workstations
- Kali Purple
- IR-Workstation
- Red Team attacker systems

---

# Part 5 — Create a Backup for a VM

## Step 17 — Select the VM in Proxmox

Click the VM you want to back up.

---

## Step 18 — Start the backup job

With the VM selected, click:

`Backup`

A backup configuration window will open.

---

## Step 19 — Choose the backup storage

In the backup window:

- select the correct storage destination

Make sure the storage has enough free space.

This is critical because backups can fail if storage is too full.

---

## Step 20 — Choose the backup mode

Choose the appropriate backup mode offered by Proxmox.

Typical options may include:

- snapshot mode
- suspend mode
- stop mode

For most live VM backups in a normal lab workflow, snapshot mode is usually preferred when supported, because it minimizes downtime.

Use a different mode only if necessary.

---

## Step 21 — Choose compression if desired

If Proxmox offers compression settings, choose the preferred project standard.

Compression may reduce backup size but can increase processing time.

---

## Step 22 — Add a note or description if available

If the backup window allows notes, include a meaningful description.

Example:

- stable baseline before detection testing
- full backup before attack scenarios
- post-agent-deployment known good state

---

## Step 23 — Start the backup

Click the button to start the backup job.

Let Proxmox complete the process.

Do not interrupt the job unless it clearly fails.

---

## Step 24 — Monitor the task log

Watch the Proxmox task output.

Make sure the backup finishes successfully.

If errors appear, do not assume the backup worked.

Read the output and verify success.

---

## Step 25 — Confirm the backup exists

After the job completes:

- go to the backup storage
- confirm the backup file exists
- confirm it is associated with the correct VM
- confirm the date and time match the backup you just created

---

# Part 6 — Repeat Backup Creation for Every VM

## Step 26 — Back up all machines

Repeat Steps 17 through 25 for every VM in the cyber range.

This includes all major infrastructure and supporting systems across:

- Red Team
- Target
- SOC

This step takes longer than snapshot creation, but it is necessary if you want full recovery capability.

---

# Part 7 — Organize and Validate the Protection Set

## Step 27 — Review all snapshots

After snapshot creation is complete, review the Snapshots tab for each VM and confirm:

- the snapshot exists
- the name is correct
- the description is meaningful

---

## Step 28 — Review all backups

After all backups finish, review the backup storage and confirm:

- each VM has a backup
- the backup task completed successfully
- no critical VM was missed
- no failed backup jobs were ignored

---

## Step 29 — Keep a record of the protected milestone

Document what the protection set represents.

Examples:

- full cyber range stable baseline
- pre-scenario baseline
- pre-detection-engineering baseline
- post-SOC-build baseline

This is important so the team knows exactly what state can be restored later.

---

# Part 8 — How to Restore a Snapshot

## Step 30 — Select the VM

In Proxmox, click the VM that needs to be restored.

---

## Step 31 — Open the Snapshots tab

Click the `Snapshots` tab.

---

## Step 32 — Select the correct snapshot

Choose the snapshot that represents the state you want.

Read the name and description carefully before restoring.

---

## Step 33 — Restore the snapshot

Click the restore / rollback option for that snapshot.

Confirm the action when prompted.

Important:

Restoring a snapshot rolls the VM back to that earlier state. Any changes made after the snapshot will be lost on that VM.

---

## Step 34 — Start the VM and validate it

After the restore:

- power on the VM if needed
- confirm it boots correctly
- confirm network configuration is correct
- confirm services behave as expected

---

# Part 9 — How to Restore a Backup

## Step 35 — Open the backup storage in Proxmox

Navigate to the storage location where backups are saved.

---

## Step 36 — Locate the correct backup file

Find the backup that belongs to the VM you want to restore.

Check:

- VM ID
- VM name
- date
- notes if present

---

## Step 37 — Start the restore process

Select the backup and choose the restore option.

Proxmox will ask where to restore it.

---

## Step 38 — Choose the restore target

Decide whether you are:

- restoring over the original VM
- restoring as a new VM for testing

Restoring as a new VM is useful if you want to test the backup without destroying the current machine.

---

## Step 39 — Complete the restore

Start the restore and wait for Proxmox to finish.

Do not interrupt the process.

---

## Step 40 — Validate the restored VM

After restore is complete:

- power on the VM
- confirm it boots
- confirm hostname and IP are correct
- confirm services work
- confirm it reflects the expected historical state

---

# Part 10 — Best Practices for This Cyber Range

## Step 41 — Snapshot before every major change

Always create a new snapshot before:

- changing firewall rules
- changing Security Onion settings
- changing time synchronization settings
- installing or removing agents
- modifying domain controllers
- running Caldera operations
- launching attack scenarios
- making mass changes across endpoints

---

## Step 42 — Create milestone backups regularly

Create full backups at major project milestones such as:

- after Red Team build completion
- after Target Environment completion
- after SOC build completion
- before the first full attack scenario
- before student use
- before major demonstrations or presentations

---

## Step 43 — Use consistent naming

Use consistent snapshot and backup names so the whole team understands them.

Good examples:

- `baseline-complete-target-env`
- `baseline-complete-soc-env`
- `pre-first-scenario`
- `pre-caldera-testing`
- `post-elastic-agent-deployment`

---

## Step 44 — Do not rely on only one protection method

Snapshots alone are not enough.

Backups alone are slower to use.

Best practice for this cyber range is to maintain both.

---

## Step 45 — Test restores occasionally

A backup is only truly trusted if it can be restored.

At intervals, perform a test restore of at least one VM to verify that the backup process is actually working.

---

# Expected Result

At the end of this procedure:

- every VM in the cyber range has a recent snapshot
- every important VM has a restorable backup
- the team can quickly roll back after failed testing
- the environment is protected before scenario execution
- the lab can recover from accidental damage, broken configuration, or destructive attack simulation

---

# Summary

This backup and snapshot process protects the full Marist Cyber Range by preserving stable restore points for every machine across the Red Team, Target, and SOC environments.

Snapshots provide fast rollback for daily testing and configuration changes.

Backups provide full recovery protection for major failures or destructive events.

Using both methods together ensures the cyber range can be safely tested, modified, rolled back, and reused for future training scenarios.
