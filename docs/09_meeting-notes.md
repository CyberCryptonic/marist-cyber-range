> **Status:** Draft   
> **Last Updated:** 2/5/26  
> **Purpose:** Provide agendas, questions, and notes for Thursday professor meetings and Monday client meetings.

# Meeting Notes Log
  
> **Purpose:** Track agendas, decisions, open questions, and action items for Thursday professor meetings and Monday client meetings.

---

## Thursday — Week 1 (Professor Meeting)

### Meeting Info
- **Date:** 2/5/26 & 2/9/26
- **Type:** Thursday Mr. Foti / Monday Central Hudson Rep
- **Attendees:** Central Hudson Group, Professor Foti, and Central Hudson Reps
- **Location/Call:** Marist University, Hancock 005

### Agenda
1.
2.
3.
4.
5.

### Questions to Confirm (use this every meeting)
#### Hardware / Virtualization
- What hypervisor are we using (VMware / Proxmox / Hyper-V)?
  
- How many hosts are available and what are the specs (CPU/RAM)?
  
- Storage model: local disks vs shared datastore (NAS/SAN)?
  
- Snapshot policy (allowed? limits? retention?) and template cloning policy?
  
- Backup/restore expectations (who owns backups, how often, where stored)?
  

#### Network / Segmentation
- Can we create multiple VLANs/zones? Who provisions them?
  
- Is there a firewall we can manage rules on? Who owns rule changes?
  
- Isolation requirements: air-gapped vs outbound for updates only?
  
- IP addressing plan: DHCP vs static, who owns DNS/DHCP?
  
- Can we mirror traffic (SPAN/TAP/vSwitch mirror) for Zeek/Suricata?
  
- Any restrictions on running vulnerable services in a DMZ zone?
  

#### Access / Accounts
- Who gets admin access (hypervisor/network)?
  
- How will students access the range (VPN + jump host vs local only)?
  
- Authentication model: AD accounts vs local accounts?
  
- Role-based access expectations (admin/instructor/student)?
  
- Logging/auditing required for admin actions?
  

#### Tooling (SIEM / Telemetry / Scenario Engine)
- SIEM preference: Splunk vs Elastic vs Security Onion (or others)?
  
- Licensing constraints or required tooling?
  
- Endpoint telemetry approach preference (Sysmon/WEF vs agent-based)?
  
- Network sensor preference (Zeek vs Suricata)?
  
- Is MITRE Caldera approved for controlled adversary emulation?
  
- Any restrictions on attacker tooling (Kali, scripts, payload hosting)?
  

#### Constraints / Safety / Compliance
- Any data handling rules (no real data, no PII, etc.)?
  
- Any restrictions on internet connectivity (none vs updates only)?
  
- Any restrictions on “malware” (simulate only, no live malware)?
  
- Required documentation artifacts for future student use?
  
- Board/client expectations for final deliverables and demo format?
  

### Notes
-

### Decisions Made (write these like final answers)
- Hypervisor:
- Host count/specs:
- Storage model:
- VLAN/segmentation approach:
- Tooling direction:
- Access model:
- Safety constraints:

### Action Items (turn these into GitHub Issues)
- [ ] (Owner) — Task — Due date
- [ ] (Owner) — Task — Due date

### Risks / Blockers
-
