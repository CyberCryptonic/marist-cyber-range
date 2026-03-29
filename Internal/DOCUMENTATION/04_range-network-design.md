# Range Network Design (v1 Draft)

> **Status:** Draft    
> **Last Updated:** 2/5/26  
> **Purpose:** Define network zones, segmentation, and safe traffic flows for the range.

## Goals
- Strong isolation from campus networks unless explicitly approved
- Clear segmentation so scenarios are safe and repeatable
- Full visibility for SOC monitoring (endpoint + network)

## Proposed Zones (VLANs/Subnets TBD)
1. **MGMT** — hypervisor management, admin jump host
2. **SOC** — SIEM, dashboards, log collectors
3. **ENTERPRISE** — AD, servers, endpoints
4. **DMZ (optional)** — internet-facing services for scenarios
5. **ATTACK** — controlled attacker host + Caldera
6. **SENSOR** — Zeek/Suricata + syslog collector (or virtual appliances)

## Traffic Policy (Default)
- Default deny between zones
- Allow only required flows documented below

## Allowed Flows (Draft)
- MGMT → hypervisor management interfaces (admin only)
- ENTERPRISE → SOC (log forwarding)
- SENSOR receives mirrored traffic (SPAN/TAP/vSwitch mirror)
- STUDENT access only via jump host (preferred)

## Open Questions for Thursday
- VLAN count and provisioning process
- Firewall control and rule ownership
- Internet access policy (updates only vs none)
- Ability to mirror traffic for sensors
