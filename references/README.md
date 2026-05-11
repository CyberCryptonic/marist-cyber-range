# References

This folder contains the source-management material used to support the Marist Cyber Range project.

The purpose of this folder is to track the official documentation, research sources, tool references, and citation exports used during the design, build, troubleshooting, and reporting process for the cyber range.

## Purpose

The Marist Cyber Range uses a combination of virtualization, networking, enterprise infrastructure, open-source security tooling, intentionally vulnerable applications, and SOC monitoring technologies.

This folder helps future teams understand:

- What official documentation was used
- Which tools supported the cyber range
- Where setup instructions and technical references came from
- How citations were managed for reports, posters, presentations, and future research
- Which sources should be reviewed before expanding or rebuilding the environment

## Files

| File | Purpose |
|---|---|
| `README.md` | Explains the purpose of the references folder |
| `source_catalog.md` | Human-readable list of important tools, documentation links, and project references |
| `zotero_workflow.md` | Explains how citations should be managed using Zotero |
| `library.bib` | BibTeX export from the shared Zotero group library |

## Source Categories

The references used for this project are organized into the following categories:

| Category | Examples |
|---|---|
| Virtualization | Proxmox VE documentation and installation material |
| Firewall / Routing | OPNsense documentation, firewall rule concepts, syslog forwarding |
| SOC / SIEM | Security Onion documentation, Fleet / Elastic Agent references, log ingestion notes |
| Red Team / Adversary Simulation | MITRE Caldera documentation, Kali Linux references |
| Vulnerable Training Applications | DVWA, OWASP Juice Shop, Metasploitable-related resources |
| Windows Enterprise Infrastructure | Active Directory, Group Policy, Windows Server, Windows Event Forwarding |
| Linux Logging | rsyslog, syslog, tcpdump, Linux service validation |
| Cybersecurity Frameworks | MITRE ATT&CK, SOC workflows, detection engineering concepts |

## Citation Management

The main citation library should be maintained in Zotero.

Recommended workflow:

1. Add official documentation or research material to the shared Zotero library.
2. Organize sources by category.
3. Export the library as `library.bib`.
4. Place the exported `library.bib` file in this folder.
5. Update `source_catalog.md` when a major tool, platform, or document becomes important to the project.

## Notes for Future Teams

Future teams should continue adding references as the cyber range grows.

Examples of future additions:

- New detection engineering references
- Updated Security Onion documentation
- Updated MITRE Caldera documentation
- Sigma rule references
- Sysmon configuration references
- Windows logging references
- Incident response playbook references
- Cloud or hybrid-range documentation if the cyber range expands beyond the current local Proxmox environment

This folder should act as the research and citation source of truth for the project.
