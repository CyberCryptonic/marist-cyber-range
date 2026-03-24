# Questions for Central Hudson:

1. What type of scenrios would you suggest for this cyber range? Are there any specific scenrios you would like to see implemented. If we had to do 5 threat scenarios, what would you do?

2. What would make this cyber range feel realistic and valuable from your perspective?

# Central Hudson Meeting Prep

## 🔹 Quick Verbal Summary (To Read in Meeting)

Over the past week, we finalized our architecture and aligned our deployment approach with the ECRL infrastructure, confirming that everything will be hosted within a single Proxmox server.

We shifted our topology to an environment-based design across Red Team, Blue Team, and SOC, while also refining user experience and finalizing tool selection.
We also updated our GitHub project section to clearly reflect progress and next steps, making it easier to track development across the team.

Additionally, we met with David to review hardware capabilities, networking constraints, and access methods, and successfully validated connectivity to the environment.

At this point, we are transitioning from the planning stage into implementation. What we are focused on now is defining the network architecture, configuring Proxmox networking, and deploying initial proof-of-concept VMs.

The core networking and segmentation has been set up within the ECRL environment, including predefined subnets for each environment and Proxmox network bridges. Our focus now is on integrating our virtual machines into that structure and ensuring proper communication between environments to support realistic attack and detection scenarios.

Moving forward, we plan to expand into full environment deployment, establish communication between systems, and begin developing realistic threat scenarios based on your input.



---

# Marist SOC Cyber Range — Weekly Breakdown (Weeks 1–13)

## Week 1 — Project Initialization
**Summary:** This week focused on establishing the foundation of the project by aligning the team, setting expectations, and creating the initial project structure.

- Formed team and clarified overall project scope (SOC Cyber Range)
- Reviewed course expectations, deliverables, and grading criteria
- Created GitHub repo + project board structure (Weeks, Issues, Workstreams)
- Established collaboration tools (GitHub, Zotero planning, communication flow)
- Began high-level brainstorming of cyber range architecture

## Week 2 — Planning & Stakeholder Prep
**Summary:** This week was centered around planning, documentation, and preparing to engage with stakeholders by defining questions and identifying unknowns.

- Developed initial project documentation:
  - Stakeholder questions
  - Deployment request draft (ECRL)
  - Semester timeline through May
- Prepared for first Central Hudson meeting
- Identified unknowns:
  - Infrastructure limitations
  - Scenario expectations
- Began defining project direction and goals

## Week 3 — Remote Access & Environment Validation
**Summary:** This week focused on validating access to the environment and troubleshooting connectivity to ensure the infrastructure could be used effectively.

- Tested VPN access into ECRL environment
- Verified connectivity to internal VMs (Splunk, etc.)
- Troubleshot xRDP and remote session issues
- Validated network reachability and service availability
- Identified infrastructure constraints and access limitations

## Week 4 — Architecture & Topology Design
**Summary:** This week involved designing the core architecture of the cyber range, including defining environments and how they interact within the network.

- Designed initial cyber range topology
- Defined three core environments:
  - Red Team (attackers)
  - Blue Team (defenders)
  - SOC/Detection (monitoring/logging)
- Began mapping IP schema and network segmentation
- Identified required VM roles and system relationships

## Week 5 — Refinement & Task Distribution
**Summary:** This week transitioned from planning to structure by refining the design, specifying technical components, and distributing responsibilities across the team.

- Made topology more technical and specific (not conceptual anymore)
- Listed exact VMs, OS types, and machine roles
- Began distributing responsibilities across team members
- Integrated interns into workflow (research + support tasks)
- Prepared refined questions for Central Hudson

## Week 6 — Infrastructure Strategy Decisions
**Summary:** This week focused on making key infrastructure decisions, including selecting the hypervisor and determining how the system would be deployed.

- Evaluated hypervisor options → decision to use Proxmox
- Planned single-server architecture with virtualization
- Discussed cloning strategy due to hardware limitations (spinning disks)
- Defined how environments will be logically separated within Proxmox

## Week 7 — VM & OS Finalization
**Summary:** This week finalized the systems that would make up the cyber range, including operating systems and the roles of each virtual machine.

- Finalized list of ~30 VMs across all environments
- Selected operating systems:
  - Kali Linux (Red Team)
  - Windows Server / Windows 10/11 (Blue Team)
  - Ubuntu (jump boxes, IR workstation)
- Confirmed Windows Education edition as substitute for Enterprise
- Mapped each VM to its functional purpose

## Week 8 — Network Segmentation & IP Planning
**Summary:** During spring break, the physical infrastructure was built and configured, and the team validated remote access by successfully connecting to the Proxmox environment.

- David assembled and configured all hardware in the ECRL
- Finalized subnet design:
  - Red Team: 10.20.10.0/24
  - Target/Blue Team: 10.20.20.0/24
  - SOC/Detection: 10.20.30.0/24
- Defined gateway structure and internal routing behavior
- Clarified role of firewall (pfSense/OPNsense)
- Established isolation between environments for realism

## Week 9 — Tooling & SOC Stack Decisions
**Summary:** This week is focused on getting fully hands-on with the environment by accessing Proxmox, understanding the system layout, and beginning initial configuration and setup of the cyber range.

- Evaluated monitoring stack options:
  - Splunk vs Security Onion
- Leaned toward Security Onion for:
  - Built-in integrations (Zeek, Suricata, ELK)
  - Scenario generation capabilities
- Defined SOC environment responsibilities:
  - Logging
  - Detection
  - Scenario execution

## Week 10 — Scenario & Attack Planning
**Summary:** This week will focus on designing realistic cyber attack scenarios and defining how different environments would interact during simulations.

- Began defining cyber attack scenarios:
  - Red Team attack simulations
  - Blue Team defensive workflows
- Considered industry-relevant scenarios (energy sector / Central Hudson)
- Planned how scenarios integrate with Security Onion
- Defined interaction between Red, Blue, and SOC environments

## Week 11 — Implementation Preparation
**Summary:** This week will prepare the team for deployment by organizing resources, templates, and configurations needed to build the environment.

- Prepared for VM deployment in Proxmox
- Planned template-based VM cloning strategy
- Defined resource allocation:
  - CPU
  - RAM
  - Storage
- Organized VM naming conventions and structure

## Week 12 — System Integration & Testing
**Summary:** This week will focus on ensuring all components work together by planning integration and testing strategies while identifying potential risks.

- Planned integration across all environments
- Defined testing strategy:
  - Network communication
  - Logging visibility
  - Attack detection validation
- Identified potential risks:
  - Hardware failure (ECRL outage history)
  - Performance bottlenecks

## Week 13 — Finalization & Presentation Prep
**Summary:** This week will wrap up the project by preparing deliverables, finalizing documentation, and getting ready to present the system at our NTIR conference as well as you at Central Hudson.

- Prepared final deliverables:
  - Demo vs presentation decision
- Organized full system walkthrough
- Created documentation for:
  - Architecture
  - Scenarios
  - Implementation process
- Practiced explaining system clearly to:
  - Professor
  - Central Hudson stakeholders


# Topology Descriptions

## Marist SOC Cyber Range Topology

**Overview:**  
Our cyber range is built on a single Proxmox server that hosts everything in one place, but inside that system we’ve separated it into three distinct environments to simulate a real enterprise setup.

**Description:**  
At a high level, we designed the environment around three main areas: Red Team, Target, and SOC/Detection. Each one sits on its own subnet, enforced by a firewall, which we ended up choosing OPNsense.

###########################################################################################
Answer to if they ask about the firewall at all: (OPNsense: It lets us replicate how real organizations separate and protect different parts of their network, which is critical for making the environment realistic. OPNsense and pfSense are very similar, but we leaned toward OPNsense because it has a more modern interface, frequent updates, and strong community support, while still giving us the same core firewall and routing capabilities.)
##########################################################################################

But this is so that they’re isolated from each other but still able to interact in a controlled and realistic way.

The Red Team environment is where all of the attacking happens. We have multiple Kali Linux machines for students, along with an instructor machine and a jump box. This is where attacks originate and get launched into the network, simulating real adversary behavior.

The Target environment is meant to look and feel like a real company network. It includes things like domain controllers, file servers, web servers, and multiple Windows user machines. We also added vulnerable applications so there’s something realistic to attack and defend. This is the environment the Blue Team is responsible for protecting.

Then we have the SOC/Detection environment, which is where all the monitoring and analysis takes place. The core of this is Security Onion, which acts as our central SOC platform by aggregating logs, alerts, and network data into one dashboard. Within this environment, Zeek provides deep network visibility by logging traffic like connections and DNS requests, while Snort detects known attack patterns using signatures. We also use a centralized Linux log server to collect system logs across machines, giving us full visibility into what’s happening during an attack.

To support realism, we also include a network traffic generator that creates normal background activity (like web browsing and file transfers), so not everything looks malicious. This forces detection tools to distinguish between real threats and normal behavior.

For simulating advanced attacks, we use MITRE Caldera, which automates adversary techniques like lateral movement and privilege escalation based on real-world attack frameworks. Finally, a cyber range orchestration server is used to automate and control scenarios, allowing us to run repeatable exercises and reset the environment when needed.

Everything is running on Proxmox, which lets us manage all of these virtual machines in one place while keeping the environments logically separated. The goal with this design was to make it as close to a real enterprise network as possible while still being controlled enough for training and experimentation.

---

## ECRL Cyber Range Architecture (David’s Setup)

**Overview:**  
David’s architecture is what actually makes our environment possible. It handles how everything is connected, how traffic flows, and how we securely access the cyber range.

**Description:**  
Starting from the outside, everything connects through the Marist network into a core OPNsense firewall. That firewall acts as the main entry point and controls what traffic is allowed in and out. From there, there’s a jump box that provides a secure way to access the environment.

Behind that, there’s a second OPNsense router that’s dedicated specifically to the cyber range. This is what separates our internal lab environment from the rest of the network and gives us more control over how traffic moves between segments.

Inside the cyber range, the network is broken up into three subnets that match our environments: Red Team, Target, and SOC. Each of these has its own gateway and is managed through the router, which keeps everything segmented but still allows communication when needed.

On the Proxmox side, networking is handled using Linux bridges. Each bridge connects to one of the environments, so when we create a VM, we just attach it to the correct bridge and it automatically ends up in the right network.

To access everything, we connect through the Marist network and either go through the jump box or directly RDP into the Proxmox server. From there, we can manage and interact with all of our virtual machines.

Overall, this setup gives us a really solid balance between security and flexibility. It keeps everything isolated and controlled, but still allows us to simulate realistic network traffic and attack scenarios.


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
