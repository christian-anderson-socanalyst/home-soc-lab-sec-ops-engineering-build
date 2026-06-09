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
