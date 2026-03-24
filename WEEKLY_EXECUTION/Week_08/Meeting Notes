# Week 08 — Meeting Notes

## Notes from meeting with Foti 3/12/26

- Remove elk stack from 

- For the demo we should record the demo in case of any delays or errors

- Demo : intro, what is a cyber range, recorded demo, leave time for questions

- Nail on our cyber range being open source in comparison to other universities that have funding

- Windows log server should be in the red

- Work on red team server and soc server first

- Before deploying we need networking for the network

- Maybe have different firewall rules depending on the day of the week

- Start giving out possible tasks for interns like doing research on specific things

- Before client meetings start planning out things like what people will say and do in the meeting

- Applying to another conference at Marist (April 9th I think?) Foti will upload assignment for when and where to apply

---

## Ben's Notes

- Stop light Status reports will be due Wednesday nights now

- Foti will review them before meetings so we can cover new content on our thursday meetings

---

## Topology

- Windows log server isn’t supposed to be part of SOC

- They aren’t called servers, they are called environments

- Entire topology is called the enterprise environment

- Each server should be renamed environments

---

## For Demo

- Record the demo for the NTIR conference so we don’t run into any issues when we’re presenting

---

## NTIR Conference

- Presenting to a group of about 10-20 people

- Will run through it a week before

- Length: 15-20 minutes

- Should present itself as a classic research presentation

- Intro, overview (current state of cyber ranges out there), research, conclusion  
--“The open source cyber range” ours was mostly open source, not crazily funded  

- Main aspect of our cyber range is that we used open source materials, so most people can do the same without needing large funding (ignoring the ECRL support we received)

- Initially, assume they don’t know anything or what a cyber range is

- Then we can get into greater details and we hope the audience can follow along (for those who might be unfamiliar with the project)

---

## Action Items

- Create a zoom meeting; invite david to review topology

---

## Implementation Discussion

- Ryan- How should we start implementation  
-Start by a little from each environment

---

## Networking Requirement

- Before we start deploying, figure out networking  
-Subnets, and how the computers are going to be talking to each other

---

## Additional Tasks

- Nate- message Cannistra for advice

---

## Notes from meeting with David 3/13/26

LINK TO RECORDING OF MEETING: https://www.youtube.com/watch?v=qgSYovAf0vY 

- Figure out hardware requirements for each VM

- Utilize network adapters in proxmox and have them take control of those subnets

- Wednesday 5pm it'll be running

---

## Server Specifications

- Server would have  
- 1TB Storage  
- 1TB System Memory  
- 32 Cores  

- Storage is expandable (rack is capable of multiple drives) and should happen sooner than later to create less of a headache

- Look into how much storage commercial Cyber Ranges offer

---

## Network Constraints

- No online connectivity for VMs

- If there is online connectivity you are restricted to 10.11.31.0/24

- Only one admin box will have internet connectivity to push updates to the other machines

- David can handle the subnetting, we have to get it to him by Monday.

---

## VPN Information

- URL Address for Marist VPN - 2620:91:0:17::0/64

- v1.marist.edu
