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
