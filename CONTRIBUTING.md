# Contributing to the Marist Cyber Range

Thank you for your interest in contributing to the Marist Cyber Range project.

This repository documents the design, build process, infrastructure, scenarios, references, and future development of a segmented cybersecurity training range.

The goal of this project is to help students, educators, and cybersecurity teams understand how to build and operate a realistic cyber range using accessible infrastructure and open-source security tooling.

## Ways to Contribute

You can contribute by:

- Improving documentation
- Adding screenshots or diagrams
- Fixing unclear setup steps
- Adding scenario playbooks
- Improving infrastructure notes
- Adding references or citations
- Creating automation scripts
- Improving validation checklists
- Reporting build issues
- Suggesting future range improvements

## Repository Areas

| Area | Purpose |
|---|---|
| `RANGE SETUP INSTRUCTIONS/` | Step-by-step environment build documentation |
| `infrastructure/` | Automation, configuration, provisioning, and baseline notes |
| `scenarios/` | Scenario playbooks and SOC training exercises |
| `references/` | Source catalog, Zotero workflow, and bibliography exports |
| `diagrams/` | Network diagrams and topology images |

## Contribution Guidelines

Before submitting a contribution:

1. Make sure the change supports the purpose of the cyber range.
2. Keep documentation clear and beginner-friendly.
3. Use consistent Markdown formatting.
4. Do not include real passwords, private keys, tokens, or secrets.
5. Do not include instructions for attacking systems outside the isolated lab.
6. Clearly state what environment your change affects.
7. Test technical instructions before submitting them when possible.
8. Include screenshots only when they help prove or explain the change.

## Scenario Contributions

Scenario playbooks should follow this structure:

`setup → execution → expected telemetry → detection → evidence → reset`

Each scenario should include:

- Overview
- Learning objectives
- Required systems
- Safety notes
- Setup steps
- Execution steps
- Expected telemetry
- Detection approach
- Evidence to capture
- Reset procedure
- Success criteria

## Infrastructure Contributions

Infrastructure contributions should explain:

- What system or environment is affected
- Why the change is needed
- What configuration is being changed
- How the change was tested
- How to roll back the change if needed

## Documentation Style

Please keep documentation:

- Clear
- Direct
- Step-by-step
- Easy for future students to follow
- Focused on authorized lab use
- Professional enough for academic and employer review

## Safety and Responsible Use

This project is for controlled cybersecurity education, research, and defensive training.

Do not contribute material that encourages unauthorized access, real-world abuse, credential theft, evasion against real systems, or activity outside an approved lab environment.

## Pull Requests

When opening a pull request, include:

- A clear summary of the change
- The folder or environment affected
- Testing or validation performed
- Screenshots if helpful
- Any known limitations

## Questions

If you are unsure where a contribution belongs, open an issue first and describe what you want to add.
