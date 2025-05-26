### 🛡️ Cybersecurity HomeLab 🛡️

![Platform](https://img.shields.io/badge/platform-HyperV-blue?logo=windows)
![Firewall](https://img.shields.io/badge/firewall-pfSense-red?logo=pfsense)
![Monitoring](https://img.shields.io/badge/monitoring-Splunk-black?logo=splunk)
![License](https://img.shields.io/github/license/gaman547/CyberSec-HomeLab)



## 🎯 Objective

Design and implement a **cybersecurity homelab** tailored for learning, testing, and experimenting in cybersecurity, networking, and system administration, while ensuring a secure and isolated environment.

## 🧠 Skills Showcased

## 🖥️ Virtualization Skills
- Proficient in setting up and managing virtual machines.
- Allocated resources (CPU, memory and storage) to virtual machines for optimal performance.
### Networking Skills
- Subnetting: Designed and implemented multiple subnets. 
- Routing: Configured pfSense to route traffic between subnets and the internet.
- Firewall Management: Created firewall rules in pfSense to control traffic flow between subnets and external network.
- Network Isolation: Ensured secure communication between isolated virtual switches.
### System Administration Skills
- OS Administration: Installed and managed Windows Server, Windows clients, and Linux systems.
- Configured Windows Server 2019 as a Domain Controller.
- Managed user accounts, groups and permissions in Active Directory.
- Configured DNS and AD Certificate Services.
- Connected client machines to the domain.
### Monitoring and Logging
- Created a dedicated monitoring VM to track network activity, analyze logs or monitor system health.
- Installed and configured Splunk Enterprise. 
### Documentation and Design
- Created detailed network diagram to document the architecture.
- Wrote this technical documentation for setup replication.

## Tools Used

- Hyper-V Manager 
- pfSense virtual firewall and router
- Splunk Enterprise 
- Microsoft Visio for designing the network diagram

## Steps

The setup I've built on a Hyper-V virtualization platform includes multiple virtual machines (VMs), virtual switches and a pfSense virtual firewall/router to manage traffic and ensure network segmentation.

 I've created the following network diagram to have a better understanding of the structure and functionality.

*Ref 1: Network Diagram*

![Network Diagram](https://github.com/gaman547/CyberSec-HomeLab/blob/main/Network%20Diagram%20HomeLab.jpg)

Here's a breakdown of the components along with a high-level step-by-step overview of the setup process, without diving deep into every single detail.

### 1. Internet and Host PC

First of all, the home router connects to the internet and provides an external connection. The Host PC acts as the virtualization platform running Hyper-V, hosting all virtual machines and virtual switches.

To use virtualization platforms like Hyper-V, we need to ensure that virtualization is enabled in the BIOS of the machine. I chose this platform because it allows running multiple operating systems as virtual machines and, in my experience, it optimally allocates resources within a Windows environment.

### 2. Virtual Switches and Subnets

The first step in setting up this network was creating the virtual switches within the Hyper-V platform. These switches form the foundation of the network, segmenting it into four distinct subnets, as illustrated below.

*Ref 2: Virtual Switches in Hyper-V*

![Virtual Switches](https://github.com/gaman547/CyberSec-HomeLab/blob/main/Virtual%20Switches%20inside%20Hyper-V.png)

*Virtual Switch WAN*

This virtual switch connects the pfSense firewall to the home router, enabling machines in other subnets to access the internet, hence we will select the switch type as external as seen below.

To create different switches for each subnet, open Hyper-V Manager on the Host PC, and then open the Virtual Switch Manager under the Actions tab.

*Ref 3: WAN*

![WAN](https://github.com/gaman547/CyberSec-HomeLab/blob/main/Virtual%20Switch%20WAN.png)

*Virtual Switch LAN* 

This virtual switch is configured as an internal type and it hosts the Kali Linux VM (10.0.1.47). The next three subnets are also configured as internal and are named accordingly. 

*Ref 4: LAN*

![LAN](https://github.com/gaman547/CyberSec-HomeLab/blob/main/Virtual%20Switch%20LAN.png)

### 3. pfSense Firewall and Router







