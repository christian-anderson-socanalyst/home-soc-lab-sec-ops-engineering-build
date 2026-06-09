# 🔐 Home SOC Lab Build
Four (4) years in security operations in an SEC-regulated environment. Hands-on work in a live cyber range. A stack of certs with more on the way.

And yet, here I am building a home lab. 😄

Definitely not to learn what Wazuh is. 

There's significant value in owning your own infrastructure. From designing the network to breaking something at 11 pm and figuring out why/how you broke it. There's a difference between this type of ownership and working within someone else's environment, and it shows in ways that are hard to fake.

My repo documents everything (network segmentation, hypervisor installation, SIEM deployment, etc.) including attack-and-defend exercises on intentionally vulnerable targets. In addition to the wins, I documented the failures, missteps, and reasoning behind every decision along the way.

Built to showcase. Documented to share. 🔧

## 🖥️ Hardware

| Device | Role | Key Specs |
|---|---|---|
| Dell Precision 7740 | Proxmox Hypervisor | Xeon E-2286M, 128GB RAM, VM dedicated 1TB NVMe SSD |
| Dell Precision 5530 | Management Workstation | Xeon E-2176M, 64GB RAM |
| MikroTik hEX (RB750Gr3) | Lab Gateway / Firewall | 5-port gigabit, RouterOS |
| MikroTik CSS610-8G-2S+IN | Managed Switch | 8x gigabit, 2x SFP+, SwOS, 802.1Q VLAN |
| CyberPower CP1000PFCLCD | UPS | 1000VA/600W, Pure Sine Wave, AVR, 10 outlets |

## 🏗️ Architecture Overview

Running a security lab in the same network as everything else (your malware samples, attack tools, and intentionally vulnerable systems) is not a good idea. Everything about this lab was designed around that one constraint.

The MikroTik hEX Firewall and CSS610 managed switch enforce VLAN separation (using IEEE 802.1Q) among the five (5) isolated network segments. There are strict inter-VLAN routing rules that dictate which segment can communicate with which. 🔒
1. Management
2. Attacker
3. Victim
4. Security Tooling
5. Fully Air-Gapped Sandbox

The virtualization layer runs on a Dell Precision 7740 mobile workstation with 128GB of RAM and a dedicated Gen 4 NVMe SSD, running Proxmox. I take snapshots before running anything in my lab, allocate resources to each VM, and have a management workstation on its own dedicated VLAN with a direct uplink to the firewall. The entire lab can be a fire on top of a dumpster fire, and the management plane stays clean. 🔥

## 🗺️ Build Phases

This is a living project. Phases get checked off when they're done, not when I come up with them. 👷

- [ ] **Phase 1: Network Foundation & Hypervisor Deployment** — 
VLAN segmentation, MikroTik configuration, and Proxmox 
installation on dedicated hardware.
- [ ] **Phase 2: Blue Team Stack** — Wazuh SIEM and Security 
Onion deployed, agents configured, and log ingestion verified.
- [ ] **Phase 3: Attack/Defend Range** — Kali Linux attacker VM 
against intentionally vulnerable targets with documented 
lab exercises.
- [ ] **Phase 4: Threat Intelligence Integration** — Live IOC 
feeds wired into the SIEM stack via AlienVault OTX, 
Abuse.ch, and MISP.
- [ ] **Phase 5: Hybrid Azure Extension** — On-premises lab 
extended into Azure via Site-to-Site VPN with cloud-native 
security tooling layered on top.

## 🛠️ Tools & Technologies

### 🌐 Network
| Tool | Description |
|---|---|
| ![MikroTik](https://img.shields.io/badge/MikroTik-RouterOS-blue) | Lab gateway, firewall, and inter-VLAN routing |
| ![MikroTik](https://img.shields.io/badge/MikroTik-SwOS-blue) | Managed switch VLAN enforcement via 802.1Q |

### 💻 Virtualization
| Tool | Description |
|---|---|
| ![Proxmox](https://img.shields.io/badge/Proxmox-VE-orange) | Hypervisor running all lab VMs on dedicated hardware |

### 🔒 Security Tools
| Tool | Description |
|---|---|
| ![Wazuh](https://img.shields.io/badge/Wazuh-SIEM-red) | Open source SIEM and EDR for log aggregation and alerting |
| ![Security Onion](https://img.shields.io/badge/Security%20Onion-NSM-green) | Network security monitoring and intrusion detection |
| ![Kali](https://img.shields.io/badge/Kali-Linux-557C94) | Dedicated attacker VM for lab exercises |

### ☁️ Coming Soon
| Tool | Description |
|---|---|
| ![Azure](https://img.shields.io/badge/Microsoft-Azure-0078D4) | Site-to-Site VPN extension for hybrid lab architecture |
| ![MISP](https://img.shields.io/badge/MISP-Threat%20Intel-lightgrey) | Self-hosted threat intelligence platform |
| ![AlienVault](https://img.shields.io/badge/AlienVault-OTX-red) | Open threat exchange IOC feed integration |
| ![Abuse.ch](https://img.shields.io/badge/Abuse.ch-IOC%20Feeds-black) | Malware and C2 indicator feeds |

---

## 📡 Network Diagram

> 🚧 Diagrams coming in Phase 1. Check back once the hardware arrives and the network is live.

<!-- 
Once complete, replace this section with:

![Network Topology](phase-1-network-foundation/diagrams/vlan-topology.png)

![Port Map](phase-1-network-foundation/diagrams/port-map.png)

### VLAN Table

| VLAN ID | Name | Purpose | Internet Access |
|---|---|---|---|
| 10 | Management | Proxmox UI, switch management | Yes |
| 20 | Victim | Intentionally vulnerable target VMs | Restricted |
| 30 | Attacker | Kali Linux | Yes |
| 40 | Security Tools | Wazuh, Security Onion | Yes |
| 99 | Isolated Sandbox | Air-gapped malware analysis | No |

-->
