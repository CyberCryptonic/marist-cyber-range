# Zotero Workflow

This file explains how references should be managed for the Marist Cyber Range project.

The goal is to keep project sources organized, reusable, and exportable for reports, posters, presentations, research papers, and future documentation.

## Tool

References should be managed using Zotero.

The shared Zotero library should contain:

- Official documentation
- Tool installation guides
- Security platform references
- Cybersecurity frameworks
- Research papers
- Vendor documentation
- Blog posts only when they provide useful implementation context

## Recommended Collections

Create the following collections inside Zotero:

- Proxmox and Virtualization
- OPNsense and Network Segmentation
- Security Onion and SOC Monitoring
- Elastic Agent and Fleet
- MITRE Caldera and Adversary Simulation
- Active Directory and Windows Server
- Linux Logging and Syslog
- Vulnerable Applications
- Cybersecurity Frameworks
- Project Reports and Presentations

## Adding a Source

When adding a source:

1. Use the browser connector when possible.
2. Confirm that the title, author, publisher, and date are correct.
3. Add a short note explaining why the source matters.
4. Add tags such as:
   - `proxmox`
   - `security-onion`
   - `opnsense`
   - `active-directory`
   - `mitre-caldera`
   - `logging`
   - `soc`
   - `cyber-range`
   - `scenario-development`

## Exporting the Library

To export the citation library:

1. Open Zotero.
2. Select the shared group library or project collection.
3. Right-click the collection.
4. Select `Export Collection`.
5. Choose `BibTeX`.
6. Save the file as `library.bib`.
7. Place the file inside the `references/` folder.
8. Commit and push the updated file to GitHub.

## File Naming

The exported citation file should use this name:

`library.bib`

Do not rename the file unless the project citation workflow changes.

## Maintenance

Future teams should update the Zotero library whenever:

- A new tool is introduced
- A major documentation source is used
- A detection framework is adopted
- A new scenario references outside material
- A report, poster, or research document is created

This keeps the repository useful as both a technical build guide and a research-backed academic project.
