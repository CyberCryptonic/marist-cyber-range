# Meeting on March 1, 2026 Notes

1. Go through the Project Plan on Github and make sure evryone is familiar with it.
2. Go over what machines we should use for the Architecture of the Project (Must be 30 minimum)
3. Come up with 5 questions for the Central Hudson meeting.
4. Redo Project Documentation in GitHub for meeting (Simplfy).
5. Maybe get topology done.
6. Research Security Onion
7. Erick adjusting Weeks 6-8 Nate adjusting weeks 9-11, & Ben Weeks 12 & 13.


---

# Meeting for Central Hudson Plan 3/3/26

## 1. Go over what was done last weeek

- We discussed the architecture of the project with david and how it will be setup/configured.  
- Created Conceptual topology.  
- Decided on what VMs will be put in place.  
- Tested the connection via RDP to ECRL servers. (Ran into hiccups when rdping, would not allow us to use the VMs). Needed a restart (unplugging the server and plugging it back in.  

---

## 2. What we are going to complete this week.

- Meeting with ECRL team to put in place our architecture design.  
- Creating new concrete topology.  
- Initial confirguration of the VMs. (Networking if needed).  
- Reviewing Project Plan and Timeline for this week.  

---

## 3. What we plan on completing the following week.

- We are currently in the process of going from a conceptual design to actually implementing defined infastructure, machine allocation, network designing, & hardware decision finalization.
- Leaning towards going with a 3 node  setup with each node carrying tools specifically for Red Teaming, Blue Teaming, & Detection and Monitoring Node (SOC / Detection Infrastructure).

---

# Questions for Central Hudson:

1. Ask about Security Onion and if we should just satick with that instead of seprating it into multiple VM's that do what Security Onion does on its own. 

2. What type of scenrios would you suggest for this cyber range? Are there any specific scenrios you would like to see implemented. Maybe one tailored to a GAS & ELECTRIC COMPANY.

3. As a final presentation did you want a demo, or a presentation on the work over the course of the semester?

4. Should we keep our firewall (pfSense/OPNsense) as a firewall and the router or have a seprate router as well?

5. What would make this cyber range feel realistic and valuable from your perspective?

---

# Architecture Concept plan:

## Node 1: Red Team Infrastructure
- Attacker VMs (Kali, C2, Exploit targets)

## Node 2: Blue Team Infrastructure
- Defender Workstations
- Log analysis
- Forensic tools

## Node 3: SOC / Detection Infrastructure
- IDS/IPS (Suricata/Snort)
- Zeek
- Splunk
- Alert pipeline
- Scenario controller

---

# RED TEAM (7)

1  Student-Attacker-01 (Kali Linux)  
2  Student-Attacker-02 (Kali Linux)  
3  Student-Attacker-03 (Kali Linux)  
4  Student-Attacker-04 (Kali Linux)  
5  Student-Attacker-05 (Kali Linux)  
6  Instructor-Attacker (Kali Linux)  
7  Red-Team-Jump-Server (Ubuntu Server)

---

# BLUE TEAM (15)

8   Primary-Domain-Server (Windows Server 2022)  
9   Backup-Domain-Server (Windows Server 2022)  
10  File-Storage-Server (Windows Server 2022)  
11  Internal-Web-Server (Windows Server 2022 / IIS)  
12  Windows10-User-01 (Windows 10 Enterprise)  
13  Windows10-User-02 (Windows 10 Enterprise)  
14  Windows10-User-03 (Windows 10 Enterprise)  
15  Windows11-User-01 (Windows 11 Enterprise)  
16  Windows11-User-02 (Windows 11 Enterprise)  
17  Windows11-User-03 (Windows 11 Enterprise)  
18  IT-Administrator-Workstation (Windows 11 Enterprise)  
19  Incident-Response-Workstation (Ubuntu Desktop)  
20  Vulnerable-Training-Server (Ubuntu Server – Juice Shop / DVWA / Metasploitable)  
21  Blue-Team-Analysis-System (Kali Purple)  
22  Blue-Team-Monitoring-System (Kali Linux – Blue Toolkit Configuration)

---

# SOC/DETECTION (11)

23  SIEM-Server (Splunk Enterprise on Ubuntu Server)  
24  Windows-Log-Server (Windows Server 2022)  
25  Linux-Log-Server (Ubuntu Server)  
26  Network-Monitoring-Sensor (Zeek on Ubuntu Server)  
27  Intrusion-Detection-System (Suricata on Ubuntu Server)  
28  Security-Monitoring-Platform (Security Onion)  
29  Firewall-and-Segmentation-Server (pfSense / OPNsense)  
30  Core-Network-Router (Ubuntu Server – Routing Configuration)  
31  Network-Traffic-Generator (Ubuntu Server – Traffic Simulation Tools)  
32  Adversary-Simulation-Server (MITRE Caldera on Ubuntu Server)  
33  Cyber-Range-Orchestration-Server (Ubuntu Server)

---

# Foti:

Feedback on Questions & Send new Project Plan & New Topology.
