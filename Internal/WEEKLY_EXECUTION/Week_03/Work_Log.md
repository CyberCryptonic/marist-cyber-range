# Week_03 — Work Log

## Tasks

- [x] Validate remote VPN connectivity
- [x] Confirm ECRL subnet routing
- [x] Test service reachability (SSH, RDP, HTTP)
- [x] Establish SSH session to Splunk VM
- [x] Diagnose xRDP session failure
- [x] Investigate Splunk service state
- [x] Perform filesystem integrity analysis
- [x] Identify remediation requirements

---

## Meeting Notes

### Summary

Week 03 focused on establishing off-campus remote access to the ECRL SOC Range environment.

VPN connectivity was successfully validated. Network-level reachability to all SOC VMs (10.11.20.205–207) was confirmed. SSH and RDP services were responding.

During Splunk VM validation, the root filesystem was found to be mounted with the ext4 `emergency_ro` flag. Write operations failed across `/tmp`, `/var`, and `/opt/splunk`. Splunk daemon was not running and could not remove its stale PID file due to read-only filesystem state.

Remount attempts were unsuccessful. Root partition `/dev/sda2` requires offline fsck or snapshot rollback via ECRL administrative intervention.

---

### Action Items

- Contact ECRL administrator regarding filesystem recovery
- Request offline fsck or snapshot rollback of Splunk VM
- Validate Splunk service post-recovery
- Resume SOC range operational validation

---

## Risks / Blockers

- Splunk VM in emergency read-only state
- Splunk service unavailable
- Desktop sessions failing due to filesystem lock
- Requires administrative intervention

**Impact:**  
SOC Range functionality currently blocked pending VM repair.

---

## Artifacts Produced

- SSH session logs
- Service validation output
- Filesystem mount state documentation
- Root partition identification (`/dev/sda2`)
- Port testing results (3389, 22, 8000)
