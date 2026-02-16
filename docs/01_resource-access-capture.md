> **Status:** Draft    
> **Last Updated:** 2/5/26  
> **Purpose:** Capture confirmed server room resources, virtualization platform, network constraints, and access model.

## Meeting Answers 2/5/26
### Compute / Hypervisor
- Hypervisor platform:
- Host count:
- CPU per host:
- RAM per host:
- GPU availability (if any):

### Storage
- Storage type (local / NAS / SAN / shared datastore):
- Total usable capacity:
- Snapshot policy (allowed? limits? retention?):
- Template/cloning policy:

### Network
- VLAN count available:
- Who provisions VLANs:
- Firewall available:
- Who manages firewall rules:
- Outbound internet (none / updates only / allowed):
- Mirroring option (SPAN/TAP/vSwitch mirror):
- IP plan approach (static/DHCP):

### Access Model
- Admin access (who, how):
- Student access method (VPN/jump host/local):
- Auth model (AD/local):
- RBAC expectations:

## Decisions Locked Today
- Access will be via VPN.

- Environment access is 24/7, but no live support (if something breaks, email ECRL).

- Multiple students can access the environment simultaneously.

- VLANs are provisioned by ECRL; the team cannot create VLANs or manage routing.

- Outbound internet access is allowed, with institutional constraints and firewall controls.

- The team is responsible for its own backups and operational management; the core Marist network cannot be modified.

- Tooling is broadly allowed (SIEM / IDS / EDR permitted); avoid tools that require paid licenses.

- Snapshots are possible, but should be used sparingly and only when necessary.

## Open Questions Remaining
- Exact hypervisor platform (VMware / Proxmox / KVM / etc.)

- Host count and per-host specifications (CPU / RAM / storage)

- Storage backend type and performance expectations

- IP management method (DHCP vs static assignments; DNS control ownership)

- Traffic mirroring options (SPAN / TAP / vSwitch mirror) for tools such as Zeek or Suricata

- Process and timeline for requesting VLAN creation and firewall rule changes

- Whether inbound access to any honeypot is allowed and how it would be implemented (NAT clarification)

- Snapshot retention policy (duration and maximum snapshot count)

- Whether VM templates or cloning (gold images) are supported

## Action Items After Meeting
- Email ECRL directors with project scope and outstanding technical questions.

- Draft the NTIR Conference abstract.

- Apply for the Marist AI Summit.

- Conduct research on the current state of cyber ranges in academia.

- Revise Central Hudson questions.

- Send updated environment/architecture diagram to Professor Algozzine and David (ECRL Networking).

- Ask Professor Foti to coordinate with Professor Algozzine regarding AI and GPU discussions (even if large GPU capacity is not required).
