# Questions for Central Hudson:

1. What type of scenrios would you suggest for this cyber range? Are there any specific scenrios you would like to see implemented. If we had to do 5 threat scenarios, what would you do?

2. What would make this cyber range feel realistic and valuable from your perspective?

# Central Hudson Meeting Prep

## 🔹 Quick Verbal Summary (To Read in Meeting)

Over the past week, we finalized our architecture and aligned our deployment approach with the ECRL infrastructure, confirming that everything will be hosted within a single Proxmox server.
We shifted our topology to an environment-based design across Red Team, Blue Team, and SOC, while also refining user experience and finalizing tool selection.
We also updated our GitHub project section to clearly reflect progress and next steps, making it easier to track development across the team.
Additionally, we met with David to review hardware capabilities, networking constraints, and access methods, and successfully validated connectivity to the environment.
At this point, we are transitioning from planning into implementation, with a focus on defining the network architecture, configuring Proxmox networking, and deploying initial proof-of-concept VMs.
The core networking and segmentation have been set up within the ECRL environment, including predefined subnets for each environment and Proxmox network bridges. Our focus now is on integrating our virtual machines into that structure and ensuring proper communication between environments to support realistic attack and detection scenarios.
Moving forward, we plan to expand into full environment deployment, establish communication between systems, and begin developing realistic threat scenarios based on your input.



---

## 1. Go over what was done last week

- Met with David to finalize infrastructure expectations and how the environment will be deployed within ECRL.  
- Confirmed that the cyber range will be hosted entirely on a single Proxmox server (1TB RAM, 32 cores, expandable storage).  
- Refined architecture approach: transitioned from multiple physical components to a fully virtualized environment inside Proxmox.  
- Updated topology understanding:
  - Environments (Red, Blue, SOC) instead of separate physical servers  
  - Entire system considered a single enterprise environment  
- Identified that nodes represent network segments rather than individual machines.  
- Discussed and began refining VM allocation across Red Team, Blue Team, and SOC environments.  
- Considered tool consolidation:
  - Moving toward Security Onion / open-source stack instead of multiple separate SIEM tools  
- Reviewed user experience design:
  - Students selecting Red vs Blue team on login  
  - Role-based access to specific environments  
- Discussed potential improvements:
  - Adding Parrot OS as an alternative to Kali (education-focused)  
  - Splitting SOC into admin vs student perspectives  
- Met with David (ECRL):
  - Reviewed hardware specs and capabilities  
  - Discussed networking constraints and subnet requirements  
  - Learned only one admin box will have internet access for updates  
- Successfully accessed ECRL infrastructure:
  - Verified connectivity via VPN  
  - Began attempting RDP access to systems  
  - Encountered RDP issues requiring troubleshooting/restarts  
- Identified critical next step: networking must be defined before full deployment  

---

## 2. What we are going to complete this week

- Finalize network architecture:
  - Define subnets for Red, Blue, and SOC environments  
  - Provide subnet plan to David for implementation  
- Begin Proxmox configuration:
  - Set up virtual networking (bridges/adapters)  
  - Prepare environment for VM deployment  
- Start initial VM deployment (proof of concept):
  - Focus on Red Team environment (Kali/Parrot OS)  
  - Focus on SOC environment (Security Onion or equivalent)  
- Continue refining topology:
  - Convert conceptual design into a fully concrete, deployable architecture  
  - Ensure alignment with Proxmox constraints  
- Improve system design decisions:
  - Finalize firewall acting as router approach  
  - Determine how environments will communicate internally  
- Begin task delegation:
  - Assign research and implementation tasks to interns  
- Prepare for demonstration:
  - Outline demo structure (intro, system walkthrough, use case, Q&A)  
  - Begin planning for recorded demo as backup  
- Update project documentation:
  - Ensure GitHub reflects current architecture and implementation progress  
  - Align project board with actual development status  

---

## 3. What we plan on completing the following week

- Begin full environment deployment:
  - Spin up additional VMs across Red, Blue, and SOC environments  
  - Expand beyond proof-of-concept into multi-system setup  
- Continue network implementation:
  - Validate communication between environments  
  - Implement firewall rules and segmentation  
  - Potentially introduce scenario-based rules (dynamic configurations)  
- Expand SOC capabilities:
  - Finalize logging, monitoring, and detection pipeline  
  - Implement centralized visibility (Security Onion or equivalent stack)  
- Develop user experience layer:
  - Define how users enter and interact with the cyber range  
  - Begin structuring role-based access (Red vs Blue team selection)  
- Start scenario development planning:
  - Incorporate feedback from Central Hudson  
  - Begin outlining 3–5 realistic threat scenarios  
- Continue documentation and reporting:
  - Maintain updated system documentation  
  - Track progress through GitHub and weekly reports  
- Prepare for upcoming presentations:
  - Continue building NTIR presentation structure  
  - Align technical implementation with research narrative (open-source cyber range focus)  

---
