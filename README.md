# 🛡️ Cybersecurity HomeLab 🛡️

![Platform](https://img.shields.io/badge/platform-HyperV-blue?logo=windows)
![Firewall](https://img.shields.io/badge/firewall-pfSense-red?logo=pfsense)
![Monitoring](https://img.shields.io/badge/monitoring-Splunk-black?logo=splunk)
![License](https://img.shields.io/github/license/gaman547/CyberSec-HomeLab)

## 🎯 Objective

Design and implement a **cybersecurity homelab** tailored for learning, testing, and experimenting in cybersecurity, networking, and system administration, while ensuring a secure and isolated environment.

## 🧠 Skills Showcased

### 🖥️ Virtualization 
* Proficient in setting up and managing virtual machines using **Hyper-V**.
* Optimized VM performance through effective allocation of **CPU, memory, and storage**.
  
### 🌐 Networking 
* **Subnetting**: Designed and deployed multiple subnets.
* **Routing**: Configured **pfSense** to route traffic between subnets and external networks.
* **Firewall Management**: Defined firewall rules to control traffic flow and ensure segmentation.
* **Network Isolation**: Achieved secure communication using isolated virtual switches.

### 🛠️ System Administration 
* Installed and managed **Windows Server 2019**, Windows 10 clients, and **Linux** machines.
* Configured **Active Directory Domain Services (AD DS)**:
  * Set up a Domain Controller.
  * Managed users, groups, and permissions.
  * Deployed **DNS** and **AD Certificate Services**.
  * Joined client machines to the domain.

### 📊 Monitoring & Logging
* Built a dedicated **monitoring VM** for:
  * Network traffic analysis
  * Log collection
  * System health monitoring
* Installed and configured **Splunk Enterprise** for log ingestion and alerting.
  
### 📝 Documentation and Design
* Created a detailed **network architecture diagram** using **Microsoft Visio**.
* Documented the entire setup process to enable easy replication.


## 🧰 Tools Used

| Tool              | Purpose                                 |
| ----------------- | --------------------------------------- |
| Hyper-V Manager   | Virtualization and VM Management        |
| pfSense           | Firewall & Network Routing              |
| Splunk Enterprise | Centralized Log Management & Monitoring |
| Microsoft Visio   | Network Diagram Design                  |


## 🛠️ Steps

The lab was built on a **Hyper-V** virtualization platform and includes multiple **virtual machines (VMs)**, **virtual switches**, and a **pfSense** virtual firewall/router to manage traffic and enforce network segmentation.

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







