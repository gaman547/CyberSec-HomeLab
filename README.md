# 🛡️ Cybersecurity HomeLab 🛡️

![Platform](https://img.shields.io/badge/platform-HyperV-blue?logo=windows)
![Firewall](https://img.shields.io/badge/firewall-pfSense-red?logo=pfsense)
![Monitoring](https://img.shields.io/badge/monitoring-Splunk-black?logo=splunk)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

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

### 🧑‍💻 System Administration 
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


## 🛠️ Setup Walkthrough

The lab was built on a **Hyper-V** virtualization platform and includes multiple **virtual machines (VMs)**, **virtual switches**, and a **pfSense** virtual firewall/router to manage traffic and enforce network segmentation.

I've created the following network diagram to have a better understanding of the structure and functionality.

*Ref 1: Network Diagram*

![Network Diagram](https://github.com/gaman547/CyberSec-HomeLab/blob/main/images/Network%20Diagram%20HomeLab.jpg)

---

Here's a breakdown of the components, followed by a high-level overview of the setup process, without diving deep into every single detail.

## 1️⃣ Internet & Host PC

The **home router** connects to the internet and provides outbound access. The **Host PC** runs **Hyper-V**, serving as the base virtualization platform where all virtual machines and virtual switches reside.

> 💡 Before using Hyper-V, ensure that **virtualization is enabled in BIOS**. Hyper-V is preferred here due to its seamless integration with Windows and efficient resource management.

## 2️⃣ Virtual Switches and Subnets

The network setup begins with creating **virtual switches** in Hyper-V, which form the segmented subnets of the lab. These provide isolation and simulate real-world network zones.

*Ref 2: Virtual Switches in Hyper-V*

![Virtual Switches](https://github.com/gaman547/CyberSec-HomeLab/blob/main/images/Virtual-Switches-inside-Hyper-V.png)

#### 🌐 Virtual Switch - WAN

This **external switch** connects pfSense to the home router, enabling internet access. It's configured in Hyper-V as an *External* type.

> 💡 To create different switches for each subnet, open Hyper-V Manager on the Host PC, and then open the Virtual Switch Manager under the Actions tab.

*Ref 3: WAN*

![WAN](https://github.com/gaman547/CyberSec-HomeLab/blob/main/images/Virtual%20Switch%20WAN.png)

#### 🔒 Virtual Switch - LAN

This **internal switch** connects the Kali Linux VM (10.0.1.47). Additional subnets are also created using internal switches to ensure complete segmentation.

*Ref 4: LAN*

![LAN](https://github.com/gaman547/CyberSec-HomeLab/blob/main/images/Virtual%20Switch%20LAN.png)

## 3️⃣ pfSense Firewall and Router

The **pfSense firewall** serves as the central hub for routing and security within the homelab environment. Deployed as a virtual machine on **Hyper-V**, it manages traffic between the WAN and multiple internal subnets, ensuring network segmentation and control.

I navigated to https://www.pfsense.org/download/ and downloaded the latest version of iso image using the below specifications.

*Ref 4: pfSense ISO*

![pfSense_ISO](https://github.com/gaman547/CyberSec-HomeLab/blob/main/images/download-pfSense-firewall-iso-image.png)




