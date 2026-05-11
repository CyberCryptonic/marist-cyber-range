# Security Policy

## Purpose

The Marist Cyber Range is an educational cybersecurity lab designed for controlled research, defensive security training, SOC workflow practice, and cyber range development.

This repository contains documentation, setup instructions, infrastructure notes, references, diagrams, and scenario playbooks for building and operating the range.

## Responsible Use

This project is intended only for authorized lab environments.

The tools, scenarios, and documentation in this repository should not be used against systems, networks, users, or organizations without explicit permission.

Offensive tooling, adversary simulation, scanning, vulnerable applications, and traffic generation should only be used inside an isolated cyber range or another approved testing environment.

## Reporting Security Issues

If you discover a security concern in this repository, please report it responsibly.

Examples of reportable issues include:

- Accidentally committed credentials
- Private keys or tokens
- Sensitive configuration data
- Unsafe scenario instructions
- Documentation that could cause harm if followed incorrectly
- Unintended exposure of internal infrastructure details
- Dangerous scripts or commands without proper warnings

## What Not to Report Publicly

Please do not open a public issue for:

- Passwords
- Private keys
- Access tokens
- Sensitive infrastructure details
- Any vulnerability that could expose a real system or account

Instead, contact the repository maintainer privately if possible.

## Supported Scope

This security policy applies to:

- Repository documentation
- Setup instructions
- Scenario playbooks
- Configuration examples
- Scripts
- Diagrams
- Reference material

This policy does not provide support for third-party tools themselves, including but not limited to:

- Proxmox VE
- Security Onion
- OPNsense
- MITRE Caldera
- Kali Linux
- Docker
- DVWA
- OWASP Juice Shop

Security issues in third-party tools should be reported to the maintainers of those projects.

## Educational Safety Boundary

All scenarios should follow these rules:

1. Run only inside the isolated cyber range.
2. Use lab-created accounts only.
3. Do not target public IP addresses or external systems.
4. Use rate limits for scanning or traffic generation.
5. Take snapshots before running scenarios.
6. Document reset steps.
7. Avoid destructive activity unless it is explicitly part of a controlled lesson.
8. Never include real credentials or sensitive personal data.

## Maintainer Response

The maintainer will review security reports and update the repository as needed.

Possible actions may include:

- Removing sensitive content
- Updating documentation
- Adding warnings
- Revising scenario steps
- Removing unsafe commands
- Improving responsible-use language
- Updating configuration examples

## Disclaimer

This project is provided for educational and research purposes. Users are responsible for ensuring that all activity is authorized, legal, and limited to approved lab environments.
