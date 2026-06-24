# multi-site-ipv6-infrastructure 
This repository features a hands-on network simulation project developed as part of my coursework at **Infnet**. The project focuses on enterprise network planning, structured IPv6 subnetting, device hardening, and static routing using exclusively the **IPv6** protocol.

## Project Overview

The primary objective of this deployment was to design and configure a corporate network topology simulating the interconnection of three geographically distributed Local Area Networks (LANs):
* **LAN Centro** (Rio de Janeiro - RJ)
* **LAN Niterói** (Rio de Janeiro - RJ)
* **LAN Av. Paulista** (São Paulo - SP)

The interstate connection was established through a backbone simulating an ISP (Internet Service Provider) cloud, ensuring high availability, edge security, and full end-to-end convergence.

## Technologies and Tools Used

* **Simulation Software:** Cisco Packet Tracer
* **Network Layer Protocol:** IPv6 (Internet Protocol version 6)
* **Network Devices:** Cisco 1941 Routers, Cisco 2960 Switches, and End-user Terminals (PCs)
* **Hardware Provisioning:** Physical installation of `HWIC-2T` serial WAN modules on the routers to establish point-to-point links.

## Network Engineering & Configurations

### 1. IPv6 Subnetting & Segmentation
Planning and structuring a global deployment using the core block `2001:DB8:CAFE::/48`. The scope was subnetted using `/64` masks to ensure a scalable network design without address overlapping:
* **LAN Centro (RJ):** `2001:DB8:CAFE:1::/64`
* **LAN Niterói (RJ):** `2001:DB8:CAFE:2::/64`
* **LAN Av. Paulista (SP):** `2001:DB8:CAFE:4::/64`
* **Interstate WAN Link (ISP Network):** `2001:DB8:CAFE:3::/64`

### 2. Device Hardening & Infrastructure Security
Configuring basic security policies directly via CLI (Cisco IOS) on the regional edge routers (`RT-RJ` and `RT-SP`) to mitigate unauthorized access:
* Plain-text password encryption: `service password-encryption`
* Privileged EXEC mode protection: `enable secret <secure_password>`
* Peripheral line protection: Securing the Console line (`line console 0`) and Virtual Terminal lines (`line vty 0 4`).

### 3. Advanced IPv6 Static Routing
Activating native IPv6 packet forwarding globally across the edge routers:
 bash
Router(config)# ipv6 unicast-routing

Manually creating static routing tables by defining precise next-hop IPv6 addresses and exit serial interfaces (Serial0/X/X). This guaranteed lean routing tables and flawless bidirectional traffic flow between Rio de Janeiro and São Paulo through the ISP cloud.

 Connectivity Validation & Verification
The topology's integrity was verified via the console using the show ipv6 route command and thoroughly audited using end-to-end ICMP (Ping) tests.

As demonstrated in the logs below, the infrastructure achieved a 100% success rate (0% packet loss) with minimal latency (1-2ms), validating the complete convergence of the multi-site network:

 Logical Topology Diagram (Cisco Packet Tracer)
![Logical Topology](screenshots/Screenshot 2026-06-24 at 15.21.01.jpg)

 End-to-End ICMP Validation (PC-1 to PC-3)
![Ping Validation PC1 to PC3](screenshots/Screenshot 2026-06-24 at 15.22.35.png)

 Return Path Routing Validation (PC-3 to PC-1)
![Ping Validation PC3 to PC1](screenshots/Screenshot 2026-06-24 at 15.23.06.png)

Practical project driven by Infnet's hands-on learning methodology.
