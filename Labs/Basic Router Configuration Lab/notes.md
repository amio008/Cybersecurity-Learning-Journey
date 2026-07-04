# Notes

## Overview

This exercise introduced the fundamentals of configuring Cisco routers using the Cisco IOS command-line interface. The goal was to configure two routers from a factory-default state, assign IPv4 addresses to their interfaces, configure basic security settings, and verify that the network was functioning correctly.

Although the topology was small, it demonstrated many of the concepts that are used repeatedly in enterprise networking and cybersecurity.

---

# Network Overview

The network consisted of:

* Two Cisco routers connected through a serial link
* One LAN connected to each router
* One host PC on each LAN

Each router acted as the default gateway for its respective subnet.

The serial connection provided communication between the two routers.

---

# Step 1 — Initial Router Setup

Before configuring the routers, any existing configuration was erased so that both devices started from a clean state.

This involved:

* Erasing the startup configuration stored in NVRAM
* Reloading the router
* Skipping the initial configuration dialog

Starting from a factory-default configuration ensures that no previous settings interfere with the current exercise.

---

# Step 2 — Basic Router Configuration

Several basic administrative settings were configured.

## Hostname

Assigning a hostname makes it much easier to identify devices when working on larger networks.

Example:

```text
hostname R1
```

---

## Disable DNS Lookup

```text
no ip domain-lookup
```

If an invalid command is entered, Cisco IOS attempts to resolve it as a hostname using DNS.

Disabling DNS lookup removes the delay caused by these failed lookups, making the CLI much more responsive during configuration.

---

## Enable Secret

```text
enable secret class
```

The **enable secret** protects Privileged EXEC mode.

Unlike the older `enable password`, the secret is stored in an encrypted form, making it the preferred method for securing administrator access.

---

## Console Password

The console password protects physical access through the console port.

Only users who know the configured password can access the router through a console connection.

---

## VTY Password

The VTY lines control remote access (such as Telnet).

Although Telnet is not considered secure today, configuring VTY authentication introduces the concept of protecting remote administrative access.

---

## MOTD Banner

A Message of the Day (MOTD) banner displays a warning before login.

In production environments this commonly serves as a legal warning indicating that only authorized users may access the device.

---

# Step 3 — Interface Configuration

Each interface was assigned an IPv4 address and activated.

Example:

```text
interface FastEthernet0/0
ip address ...
no shutdown
```

One important observation was that interfaces remain **administratively down** until the `no shutdown` command is issued.

Without enabling the interface, communication is impossible regardless of the IP configuration.

---

# Step 4 — Serial Connection

The routers communicated using a serial link.

The DCE side was configured with

```text
clock rate 64000
```

The DCE device supplies clocking for the connection, while the DTE device receives it.

This was my first practical exposure to the difference between DCE and DTE devices.

---

# Step 5 — Host Configuration

Each PC was assigned:

* IPv4 address
* Subnet mask
* Default gateway

The default gateway was configured as the IP address of the router interface connected to that LAN.

Without a correct default gateway, hosts cannot communicate outside their local network.

---

# Step 6 — Verification

After configuration, several Cisco IOS commands were used to verify the network.

## show ip interface brief

This command quickly displays:

* Interface names
* Assigned IP addresses
* Administrative status
* Operational status

It is one of the fastest ways to determine whether an interface is functioning correctly.

---

## show ip route

The routing table contained only **directly connected** networks.

This demonstrated that Cisco routers automatically install routes for networks connected to active interfaces.

No static routes or routing protocols had been configured at this stage.

---

## ping

Ping was used to verify connectivity between:

* PCs and their default gateways
* Router-to-router serial interfaces

Successful replies confirmed that the interface configurations and addressing were correct.

---

# Reflection

One observation from this exercise was that the two LANs could **not** communicate with each other.

Each router knew only about its own directly connected networks.

Neither router had a route to the remote LAN, so packets destined for those networks were discarded.

This demonstrated why routers require either:

* Static routes, or
* Dynamic routing protocols such as RIP, OSPF, or EIGRP

to communicate beyond directly connected networks.

---

# Cybersecurity Perspective

Although this exercise focused on networking fundamentals, the same concepts are used daily in cybersecurity.

Understanding router configuration is valuable when:

* Investigating network incidents
* Troubleshooting connectivity problems
* Performing packet analysis
* Deploying firewalls
* Building penetration testing labs
* Understanding how attackers move through networks

Networking knowledge provides the foundation for nearly every area of cybersecurity.

---

# Key Takeaways

* Cisco IOS follows a hierarchical configuration model.
* Interfaces remain disabled until explicitly enabled.
* Directly connected networks automatically appear in the routing table.
* Running configuration is stored in RAM, while startup configuration is stored in NVRAM.
* The DCE side of a serial connection must provide clocking.
* Verification commands are essential for troubleshooting.
* Routers require additional routing information to reach remote networks.

---

# Next Topics

This exercise provides the foundation for more advanced networking concepts, including:

* Static Routing
* Dynamic Routing (RIP, OSPF, EIGRP)
* VLANs
* Inter-VLAN Routing
* ACLs
* NAT
* DHCP
* Network security
* Packet analysis with Wireshark
