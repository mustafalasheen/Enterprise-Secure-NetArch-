# Enterprise Network Security Architecture

## Project Overview

This project presents a robust and scalable enterprise network security architecture, meticulously designed and simulated using Cisco Packet Tracer v9.0.0. The primary objective is to establish a secure, resilient, and multi-protocol network environment capable of supporting diverse organizational needs while adhering to contemporary security best practices. This architecture integrates advanced networking concepts, including IPv4 and IPv6 addressing, sophisticated switching technologies, dynamic routing protocols, and a comprehensive suite of layered security mechanisms.

The network infrastructure is logically segmented into two distinct yet interconnected domains:

*   **Enterprise Internal IPv4-Only Network**: This domain represents the core internal operations, characterized by strict access controls and centralized management.
*   **Service-Oriented Dual-Stack (IPv4 & IPv6) Network**: This domain is designed to host enterprise application services, offering seamless connectivity through both IPv4 and IPv6 protocols.

## Network Topology

The foundational design of this enterprise network is visually represented in the topology diagram below. This diagram illustrates the logical and physical interconnections between various network devices, highlighting the segmentation into the IPv4-only and dual-stack domains.

<img width="968" height="443" alt="Enterprise Network Topology Diagram" src="https://github.com/user-attachments/assets/20514efa-c3d2-4164-9960-9d20cd96ebba" />

*Figure 1: Comprehensive Enterprise Network Topology Diagram*

## Architectural Design and Implementation

### Left Side – IPv4-Only Domain: Internal Enterprise Network

This segment of the network is dedicated to internal enterprise operations, emphasizing stringent access control and centralized monitoring capabilities. It is engineered to provide a secure and stable environment for critical business functions.

#### Addressing Scheme

*   **IPv4 Address Space**: `10.11.12.0/24` is utilized across this domain, ensuring efficient address allocation and network segmentation.

#### Key Features

*   **DHCP Services**: Automated IP address assignment for end-devices, streamlining network administration.
*   **Dynamic Routing**: OSPFv2 (Open Shortest Path First version 2) is deployed for IPv4 routing, ensuring optimal path selection and rapid convergence.
*   **Centralized Management and Security**: Integration of essential services for enhanced operational control and threat intelligence:
    *   **NTP (Network Time Protocol)**: Synchronized timekeeping across all devices for accurate logging and event correlation.
    *   **Syslog**: Centralized logging mechanism for comprehensive event monitoring and security auditing.
    *   **AAA (Authentication, Authorization, Accounting)**: Robust framework for managing user access and activities within the network.

### Right Side – Dual-Stack (IPv4 & IPv6) Domain: Service-Oriented Network

This domain is designed to support both IPv4 and IPv6 connectivity, hosting critical enterprise application services. It facilitates a smooth transition to IPv6 while maintaining full compatibility with existing IPv4 infrastructure.

#### Addressing Scheme

*   **IPv6 Prefix**: `2000:12:34::/64` is implemented for IPv6 addressing, supporting a vast number of devices and future expansion.
*   **IPv6 Configuration**: A combination of SLAAC (Stateless Address Autoconfiguration) and Stateless DHCP for IPv6 clients is employed for flexible and efficient IPv6 address management.
*   **IPv4 Addressing**: Utilized for routing and ensuring service reachability, maintaining interoperability with IPv4-dependent systems.

#### Routing Protocols

*   **OSPFv2 for IPv4**: Continues to be used for IPv4 routing within this domain.
*   **IPv6 Connectivity**: Achieved through IPv6 tunneling over IPv4, providing a transitional mechanism for IPv6 communication across an IPv4-centric backbone.

#### Enterprise Services Hosted

This domain hosts a suite of essential enterprise services, all secured according to defined security policies:

*   **DNS Server (Domain Name System)**: Facilitates name resolution for both internal and external resources.
*   **Web Server (HTTP / HTTPS)**: Provides secure web-based application access.
*   **Mail Server (SMTP / POP3)**: Manages email communication for the enterprise.
*   **FTP Server (File Transfer Protocol)**: Enables secure file transfer operations.

## Advanced Security and Connectivity Features

This architecture incorporates a multi-layered security approach, safeguarding the network from various threats and ensuring robust connectivity.

### Layer 2 Security Enhancements

*   **VLAN Segmentation**: Logical separation of network traffic into User, Management, and Trunk VLANs to enhance security and performance.
*   **802.1X Authentication**: Port-based network access control, ensuring only authorized devices can connect to the network.
*   **Port Security**: Limits the number of MAC addresses allowed on a port, mitigating MAC flooding attacks.
*   **DHCP Snooping**: Prevents rogue DHCP servers and protects against DHCP starvation attacks.
*   **Dynamic ARP Inspection (DAI)**: Validates ARP packets to prevent ARP spoofing and poisoning attacks.
*   **Spanning Tree Protocol (STP) Security**: Implementation of:
    *   **PortFast**: Immediately brings a port to the forwarding state, bypassing listening and learning states.
    *   **BPDU Guard**: Disables ports that receive BPDUs, preventing unauthorized switches from affecting the STP topology.
*   **Blackhole VLAN**: Unused switch ports are isolated into a blackhole VLAN, minimizing potential attack vectors.

### Layer 3 & Perimeter Defense

*   **Zone-Based Policy Firewall (ZBF)**: Deployed to enforce granular security policies between different network zones.
*   **Access Control Lists (ACLs)**: Configured to filter network traffic based on specified criteria, enhancing network access control.
*   **IOS Intrusion Prevention System (IPS)**: Provides real-time threat detection and prevention capabilities on network devices.
*   **Cisco ASA Firewall**: Dedicated firewall for DMZ protection, securing public-facing services.
*   **Secure Wireless Access**: Implementation of WPA2 / WPA3 protocols for robust wireless network security.

### Management and AAA Security

*   **AAA Authentication**: Utilizes a hierarchical authentication mechanism:
    *   **TACACS+**: Primary authentication protocol for device administration.
    *   **RADIUS**: Secondary authentication protocol, offering flexibility and redundancy.
    *   **Local Authentication**: Fallback mechanism for continued access in case of external server unavailability.
*   **Role-Based Access Control (RBAC)**: Assigns specific privileges based on user roles, ensuring administrative separation of duties.
*   **Customized Privilege Levels**: Granular control over administrative access to network devices.

### Inter-Site and IPv6 Connectivity

*   **Site-to-Site IPSec VPN**: Establishes secure, encrypted communication tunnels over IPv4 between remote sites (R4 and R6).
*   **Encrypted Inter-Domain Communication**: Ensures confidentiality and integrity of data exchanged between different network segments.
*   **IPv6 Tunneling over IPv4**: Facilitates IPv6 communication across an IPv4-only routed backbone, enabling end-to-end IPv6 connectivity between domains.

## Project Objectives

The successful implementation of this architecture addresses several key objectives:

### 1. Establish a Dual-Stack Network Environment

*   Deployment of IPv4 addressing (`10.11.12.0/24`) across all routers and inter-router links.
*   Implementation of IPv6 addressing (`2000:12:34::/64`) on the right-side routers (Branch2: R1, R2, R3).
*   Configuration of DHCP for IPv4 hosts and SLAAC for IPv6 hosts.
*   Enabling IPv6 tunneling over IPv4 to bridge connectivity gaps.

### 2. Implement Secure Layer 2 Switching

*   Configuration of VLANs for user, management, and trunk traffic.
*   Application of comprehensive Layer 2 security features, including 802.1X authentication, Port Security, DHCP Snooping, Dynamic ARP Inspection (DAI), and STP security (PortFast, BPDU Guard).
*   Isolation of unused switch ports into a blackhole VLAN for enhanced security.

### 3. Configure Dynamic Routing

*   Deployment of OSPFv2 (IPv4) on both the left-side and right-side networks where required.
*   Achievement of IPv6 routing through tunneling mechanisms.
*   Configuration of static routing for networks behind the ASA firewall.

### 4. Deploy Core Network Services

*   Configuration of an authenticated NTP server for the left-side network and Router R5 as an NTP Master for the right-side.
*   Deployment of a Syslog server for centralized logging.
*   Implementation of essential enterprise servers: DNS, Web (HTTP/HTTPS), Mail (SMTP/POP3), and FTP.

### 5. Strengthen Network Defense

*   Configuration of ZBF on Branch1-Edge to control various protocols (ICMP, HTTP/HTTPS, DNS, FTP).
*   Deployment of IOS IPS on the ISP Router with stateful inspection capabilities.
*   Application of IPv6 ACLs on Branch2-R2 to restrict unauthorized IPv6 inter-VLAN traffic.
*   Configuration of Cisco ASA firewall policies for INSIDE → DMZ and OUTSIDE → DMZ traffic flows.

## Tools and Technologies Utilized

This project leverages industry-standard tools and technologies to simulate and implement the network architecture:

*   **Cisco Packet Tracer 9.0.0**: The primary simulation environment for network design and testing.
*   **Cisco IOS Routers and Switches**: Emulated Cisco networking devices for routing and switching functionalities.
*   **Cisco ASA Firewall**: Simulated Adaptive Security Appliance for advanced perimeter security.
*   **IPv4 / IPv6 Dual-Stack Networking**: Comprehensive support for both IP addressing schemes.
*   **IPSec VPN**: Implementation of secure virtual private networks for inter-site connectivity.

## Repository Contents

The repository is structured to provide all necessary files for understanding, replicating, and extending this network security architecture:

*   **Packet Tracer Topology File**: The `.pkt` file containing the complete network simulation.
*   **Router and Switch Configuration Files**: Detailed configuration scripts for all network devices.
*   **Documentation and Network Diagrams**: Supplementary documents explaining design choices and visual representations of the network.

## Subnetting and VLAN Allocation

To provide a clear understanding of the network's addressing scheme and VLAN segmentation, the following tables detail the IPv4 and IPv6 subnet allocations for both the left-side (IPv4-Only) and right-side (Dual-Stack) domains, as well as point-to-point links and ASA interfaces.

### Left Side - IPv4 Subnetting

| VLAN ID | VLAN Name             | IPv4 Subnet       |
|---------|-----------------------|-------------------|
| 10      | Branch1-HR            | 10.11.12.0/29     |
| 20      | Branch1-NS            | 10.11.12.8/29     |
| 30      | Branch1-PR            | 10.11.12.16/29    |
| 40      | Branch1-SOC           | 10.11.12.24/29    |
| 50      | Branch1-IT            | 10.11.12.32/29    |
| 60      | Branch1-Sales         | 10.11.12.40/29    |
| 70      | Branch1-Ops           | 10.11.12.48/29    |
| 80      | Branch1-QA            | 10.11.12.56/29    |
| 90      | Branch1-Management-A  | 10.11.12.64/29    |
| 100     | Branch1-Management-B  | 10.11.12.72/29    |
| 110     | Branch1-Management-C  | 10.11.12.80/29    |
| 120     | Branch1-Wireless      | 10.11.12.88/29    |

### Left Side - IPv6 Subnetting (Placeholder for future expansion or specific use cases)

| VLAN ID | VLAN Name             | IPv6 Subnet           |
|---------|-----------------------|-----------------------|
| 10      | Branch1-HR            | 2000:12:34:20::/64    |
| 20      | Branch1-NS            | 2000:12:34:21::/64    |
| 30      | Branch1-PR            | 2000:12:34:22::/64    |
| 40      | Branch1-SOC           | 2000:12:34:23::/64    |
| 50      | Branch1-IT            | 2000:12:34:24::/64    |
| 60      | Branch1-Sales         | 2000:12:34:25::/64    |
| 70      | Branch1-Ops           | 2000:12:34:26::/64    |
| 80      | Branch1-QA            | 2000:12:34:27::/64    |
| 90      | Branch1-Management-A  | 2000:12:34:28::/64    |
| 100     | Branch1-Management-B  | 2000:12:34:29::/64    |
| 110     | Branch1-Management-C  | 2000:12:34:30::/64    |
| 120     | Branch1-Wireless      | 2000:12:34:31::/64    |

### Right Side - Dual-Stack Subnetting (IPv4 & IPv6)

| VLAN ID | VLAN Name             | IPv6 Subnet           | IPv4 Subnet         |
|---------|-----------------------|-----------------------|---------------------|
| 10      | Branch2-HR            | 2000:12:34:1::/64     | 10.11.12.176/29     |
| 20      | Branch2-NS            | 2000:12:34:2::/64     | 10.11.12.184/29     |
| 30      | Branch2-PR            | 2000:12:34:3::/64     | 10.11.12.192/29     |
| 40      | Branch2-SOC           | 2000:12:34:4::/64     | 10.11.12.200/29     |
| 50      | Branch2-IT            | 2000:12:34:5::/64     | 10.11.12.208/29     |
| 60      | Branch2-Sales         | 2000:12:34:9::/64     | 10.11.12.216/29     |
| 70      | Branch2-Management-A  | 2000:12:34:6::/64     |                     |
| 80      | Branch2-Management-B  | 2000:12:34:7::/64     |                     |
| 90      | Branch2-Management-C  | 2000:12:34:8::/64     |                     |
| 100     | Branch2-Native1       |                       |                     |
| 110     | Branch2-Native2       |                       |                     |
| 120     | Branch2-Native3       |                       |                     |
| 130     | Branch2-Management-A-V4 |                     | 10.11.12.152/29     |
| 140     | Branch2-Management-B-V4 |                     | 10.11.12.160/29     |
| 150     | Branch2-Management-C-V4 |                     | 10.11.12.168/29     |

### Point-to-Point Links

| Link Description | IPv4 Subnet       |
|------------------|-------------------|
| P2P Link 1       | 10.11.12.104/29   |
| P2P Link 2       | 10.11.12.104/30   |
| P2P Link 3       | 10.11.12.108/30   |
| P2P Link 4       | 10.11.12.112/29   |
| P2P Link 5       | 10.11.12.112/30   |
| P2P Link 6       | 10.11.12.116/30   |
| P2P Link 7       | 10.11.12.120/29   |
| P2P Link 8       | 10.11.12.120/30   |
| P2P Link 9       | 10.11.12.124/30   |
| P2P Link 10      | 10.11.12.128/29   |
| P2P Link 11      | 10.11.12.128/30   |
| P2P Link 12      | 10.11.12.132/30   |
| P2P Link 13      | 10.11.12.136/29   |
| P2P Link 14      | 10.11.12.136/30   |
| P2P Link 15      | 10.11.12.140/30   |
| P2P Link 16      | 10.11.12.144/29   |
| P2P Link 17      | 10.11.12.144/30   |
| P2P Link 18      | 10.11.12.148/30   |

### ASA Firewall Interfaces

| Interface Name | IPv4 Subnet       |
|----------------|-------------------|
| INSIDE         | 10.11.12.232/29   |
| DMZ            | 10.11.12.240/29   |
| OUTSIDE        | 10.11.12.248/29   |
