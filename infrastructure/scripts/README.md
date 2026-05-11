# Scripts

This folder is reserved for automation scripts used to configure, validate, maintain, or reset the Marist Cyber Range.

## Purpose

Scripts should make the range easier to rebuild, validate, and operate.

Future scripts may support:

- Active Directory user creation
- Active Directory group creation
- Endpoint configuration
- Linux logging configuration
- Elastic Agent validation
- Security Onion health checks
- Firewall rule documentation
- Scenario setup
- Scenario reset
- Backup validation
- Traffic generation

## Script Categories

Recommended organization:

| Folder | Purpose |
|---|---|
| `windows/` | PowerShell scripts for Windows systems |
| `linux/` | Bash scripts for Linux systems |
| `validation/` | Scripts that confirm services, logs, agents, and connectivity |
| `scenario-reset/` | Scripts used to restore systems after training scenarios |
| `traffic-generation/` | Controlled background traffic scripts |

## Script Documentation Standard

Every script should include:

- Script name
- Author or team
- Purpose
- Supported operating system
- Required permissions
- Expected inputs
- Expected outputs
- Safety notes
- Rollback instructions if the script changes system state

## Safety Rules

Scripts should not be added unless they are safe for the cyber range.

Do not commit scripts that:

- Contain real passwords
- Contain private keys
- Disable security controls without explanation
- Make destructive changes without rollback notes
- Launch high-volume traffic without rate limits
- Execute offensive actions outside the isolated cyber range

## Naming Convention

Use clear names.

Examples:

- `create_ad_users.ps1`
- `enable_windows_logging.ps1`
- `configure_rsyslog_securityonion.sh`
- `check_elastic_agent_health.ps1`
- `validate_securityonion_ports.sh`
- `generate_background_http_traffic.sh`

## Notes

Scripts should be tested in the lab before being committed to the repository.
