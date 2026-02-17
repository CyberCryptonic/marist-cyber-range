# Week_03 — Timeline

## Phase 1 — Remote Connectivity Validation
- Connected to Marist VPN via Cisco Secure Client
- Verified VPN route injection (10.0.0.0/8)
- Confirmed reachability of:
  - 10.11.20.205 (Splunk VM)
  - 10.11.20.206 (Target Box)
  - 10.11.20.207 (Attack Box)

## Phase 2 — Service Layer Validation
- Tested TCP/3389 (RDP) — confirmed listening
- Tested TCP/22 (SSH) — confirmed accessible
- Tested TCP/8000 (Splunk Web) — not listening
- Established SSH session to Splunk VM

## Phase 3 — Infrastructure Diagnosis
- Verified xRDP service running
- Confirmed Splunk daemon not running
- Identified stale PID file
- Diagnosed root filesystem mounted with ext4 flag `emergency_ro`
- Confirmed write operations failing system-wide
- Identified root device: `/dev/sda2`
- Attempted remount — unsuccessful
- Determined offline fsck or snapshot rollback required
