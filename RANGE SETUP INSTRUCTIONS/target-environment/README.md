# Target Environment Setup

This environment simulates a real enterprise network.

## Status

🚧 IN PROGRESS

The Target Environment is operational and mostly complete, but final validation and cleanup are still ongoing.

## Build Progress

- ✅ IP Configuration Defined
- ✅ Domain Controller Setup
- ✅ Initial Active Directory Configuration
- ✅ Windows 10 Deployment
- ⚠️ Windows 11 Validation In Progress
- ✅ File Server Deployment
- ✅ Group-Based Access Control Implemented
- ⚠️ OU / Group Cleanup In Progress
- ❌ Final Full Validation Not Yet Completed

## Build Order

1. `ip_configuration.md`
2. `phase_01_networking.md`
3. `phase_02_active_directory.md`
4. `phase_03_ad_structure_gpo.md`
5. `phase_04_file_server.md`

## Systems Included

- Primary-Domain-Server
- File-Server
- Windows 10 Workstations
- Windows 11 Workstations

## Current Completion State

The Target Environment is fully operational but still undergoing refinement.

### Completed
- Active Directory deployment
- Domain-joined endpoints
- File server with enterprise share structure
- Group-based permissions model
- Target subnet IP planning

### In Progress
- Windows 11 validation
- OU and group cleanup
- final permission tuning

### Next Phase
- SOC / Detection Environment integration

## Goal

To replicate a realistic enterprise network for defensive cybersecurity training and future SOC visibility.
