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

![Network Diagram](https://github.com/gaman547/CyberSec-HomeLab/blob/main/images/Network-Diagram-HomeLab.jpg)

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

![WAN](https://github.com/gaman547/CyberSec-HomeLab/blob/main/images/Virtual-Switch-WAN.png)

#### 🔒 Virtual Switch - LAN

This **internal switch** connects the Kali Linux VM (10.0.1.47). Additional subnets are also created using internal switches to ensure complete segmentation.

*Ref 4: LAN*

![LAN](https://github.com/gaman547/CyberSec-HomeLab/blob/main/images/Virtual-Switch-LAN.png)

## 3️⃣ pfSense Firewall and Router

The **pfSense firewall** serves as the central hub for routing and security within the homelab environment. Deployed as a virtual machine on **Hyper-V**, it manages traffic between the WAN and multiple internal subnets, ensuring network segmentation and control.

I started by downloading the latest pfSense ISO image from the [official website](https://www.pfsense.org/download/), using the bellow specifications.

*Ref 4: pfSense ISO*

![pfSense_ISO](https://github.com/gaman547/CyberSec-HomeLab/blob/main/images/download-pfSense-firewall-iso-image.png)

Next I've created the **pfSense** virtual machine with the following configuration.

* Name: pfSense
* Generation: Gen 2
* CPU: 2 vCPU
* Memory: 4 GB
* Storage: 40 GB (dynamically allocated)
* Network Adapter: WAN

> 💡  Using Generation 2 ensures compatibility with modern system requirements and allows UEFI boot support.

Upon creation, I edited the virtual machine settings and made the following changes.

* Disabled Secure Boot
* Changed boot order
* Added the remaining network adapters

*Ref 5: pfSense VM Settings*

![pfSense_Settings](https://github.com/gaman547/CyberSec-HomeLab/blob/main/images/pfSense-VM-Settings.png)

Upon initial boot, pfSense prompts for instalation and partitioning the disk. I made sure to partition the disk with the following settings.

* AUTO (ZFS) - Guided Root-on-ZFS
* Stripe - No Redundancy

After reboot, pfSense prompts for interface assignments.

> 💡 When asked if VLANs need to be set up first, press n.

Next I manually setup the following interfaces.

* WAN = hn0
* LAN = hn1
* OPT1 = hn2 (Monitoring)
* OPT2 = hn3 (AD)
* OPT3 = hn4 (Vulnerable Machines)

*Ref 6: pfSense interfaces*

![pfSense_interfaces](https://github.com/gaman547/CyberSec-HomeLab/blob/main/images/pfSense-interface-config.png)

Each interface is configured with a static IP address appropriate for its subnet. The WAN interface got the IP address from my home router network.
The Default LAN ip addres is 192.168.1.1/24 while the other interfaces are not configured yet.

Next I selected option 2 as seen bellow.

*Ref 7: pfSense LAN setup*

![pfSense_LAN_Setup](https://github.com/gaman547/CyberSec-HomeLab/blob/main/images/pfSense-LAN-setup.png)

Afterwards I selected the LAN interface and configured it as follows.

* Configure IPv4 address LAN interface via DHCP? = n
* Enter the new LAN IPv4 address = 10.0.1.1
* Enter the new LAN IPv4 subnet bit count = 24

*Ref 8: pfSense LAN interface configuration* 

![pfSense_LAN_interface](https://github.com/gaman547/CyberSec-HomeLab/blob/main/images/pfSense-LAN-interface.png)

> 💡 I pressed Enter as we do not want any upstream gateway for LAN interface.

I continued with the following configuration.

* Configure IPv6 address LAN interface via DHCP6 = n
* For the new LAN IPv6 address question = press ENTER
* Do you want to enable DHCP server on LAN? = y
* Enter the start address of the IPv4 clint address range = 10.0.1.100
* Enter the end address of the IPv4 client address range = 10.0.1.200
* Do you want to revert to HTTP as the webConfigurator protocol = n

*Ref 9: pfSense LAN iterface DHCP configuration*

![pfSense_LAN_interface_DHCP](https://github.com/gaman547/CyberSec-HomeLab/blob/main/images/pfSense-LAN-interface-dhcp.png)

> 💡 I followed the same patern for Monitoring and Vulnerable Machines interfaces.


















