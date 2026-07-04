# Basic Router Configuration

> **Note**
>
> This repository contains my own notes, commands, explanations, and screenshots from a hands-on networking exercise completed as part of my cybersecurity self-learning journey. No proprietary course materials or starter files are included.

---

## Overview

This exercise focuses on configuring Cisco routers from a factory-default state using Cisco Packet Tracer. The objective was to gain practical experience with the Cisco IOS command-line interface (CLI), configure a small routed network, and verify end-to-end connectivity.

Although the network is intentionally simple, it introduces many of the concepts that form the foundation of networking and cybersecurity, including IP addressing, interface configuration, routing tables, device management, and basic troubleshooting.

---

## Learning Objectives

After completing this exercise, I was able to:

* Configure Cisco routers from their default state
* Navigate Cisco IOS using the command-line interface
* Configure router hostnames and secure administrative access
* Configure Ethernet and Serial interfaces
* Assign IPv4 addresses to routers and hosts
* Understand the purpose of DCE and DTE serial connections
* Save and restore router configurations
* Verify network connectivity using Cisco verification commands
* Perform basic network troubleshooting

---

## Network Topology

The lab consists of two routers connected through a serial link, with each router serving a separate local network.

```
PC1
 |
 |
R1 ----------- R2
 |             |
 |             |
LAN 1        LAN 2
```

*A screenshot of the topology is available in the `images/` directory.*

---

## Skills Practiced

### Cisco IOS

* User EXEC mode
* Privileged EXEC mode
* Global Configuration mode
* Interface Configuration mode
* Line Configuration mode

### Router Configuration

* Hostname configuration
* EXEC password configuration
* Console password configuration
* VTY (Telnet) password configuration
* Message of the Day (MOTD) banner
* Interface activation using `no shutdown`
* Serial interface clock rate configuration
* Configuration persistence (`running-config` → `startup-config`)

### IPv4 Networking

* Static interface addressing
* Subnet masks
* Default gateways
* Directly connected routes
* Layer 3 connectivity verification

---

## Verification Performed

The following commands were used to validate the configuration and troubleshoot the network.

| Command                              | Purpose                                           |
| ------------------------------------ | ------------------------------------------------- |
| `show ip interface brief`            | Verify interface status and assigned IP addresses |
| `show ip route`                      | Verify routing table entries                      |
| `show running-config`                | Review the active configuration                   |
| `ping`                               | Test Layer 3 connectivity between devices         |
| `copy running-config startup-config` | Save the configuration to NVRAM                   |

Verification included:

* Successful interface activation
* Correct IPv4 addressing
* Reachability between hosts and their default gateways
* Successful communication between both routers
* Validation of directly connected routes

---

## Key Concepts Learned

### Running Configuration vs Startup Configuration

One of the most important concepts introduced during this exercise was understanding the difference between:

* **Running Configuration** – Stored in RAM and lost after a reboot unless saved.
* **Startup Configuration** – Stored in NVRAM and loaded during device startup.

Saving the configuration ensures that router settings persist after a restart.

---

### Directly Connected Routes

After configuring interfaces, Cisco IOS automatically adds connected networks to the routing table.

Viewing these entries using `show ip route` provided a practical understanding of how routers build routing tables before any dynamic routing protocols are introduced.

---

### Serial Connections

The serial link between the routers demonstrated the relationship between:

* DCE devices (provide clocking)
* DTE devices (receive clocking)

This explains why the DCE side requires a configured clock rate before communication can occur.

---

## Cybersecurity Relevance

Although this is primarily a networking exercise, these concepts are fundamental to cybersecurity.

Understanding router configuration is essential for:

* Network troubleshooting
* Packet analysis
* Firewall deployment
* Network segmentation
* Secure infrastructure design
* Incident response
* Network reconnaissance
* Penetration testing labs

A strong understanding of networking provides the foundation for understanding how attacks move across networks and how defensive controls are implemented.

---

## Repository Contents

```
Basic-Router-Configuration/
│
├── README.md
├── commands.md
├── notes.md
└── images/
    ├── topology.png
    ├── show-ip-route.png
    ├── show-ip-interface-brief.png
    └── ping-test.png
```

---

## Lessons Learned

Some of the most valuable takeaways from this exercise include:

* Interfaces remain administratively down until explicitly enabled using `no shutdown`.
* Routers automatically learn directly connected networks.
* Verifying configurations is just as important as applying them.
* Correct IP addressing is essential for successful communication.
* Small configuration mistakes can completely prevent network connectivity.
* Understanding the CLI is critical before progressing to advanced networking and security topics.

---

## Next Steps

This exercise serves as the starting point for more advanced networking topics, including:

* Static Routing
* Dynamic Routing (RIP, OSPF, EIGRP)
* VLANs
* Inter-VLAN Routing
* Access Control Lists (ACLs)
* Network Address Translation (NAT)
* DHCP
* Packet analysis using Wireshark
* Enterprise network security

---

## Disclaimer

This repository is intended solely to document my personal learning process. All documentation, explanations, notes, and screenshots are my own. No proprietary instructional materials, lab handouts, or starter Packet Tracer files are included.
