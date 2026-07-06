# Blue-Team-Home-Lab

Enterprise-style cybersecurity home lab built using **Proxmox VE**, **pfSense**, **Windows Server 2022**, **Active Directory**, **Wazuh SIEM**, and **Linux** to simulate a small business environment.

The goal of this project is to demonstrate enterprise infrastructure deployment, virtualization, Windows domain administration, network segmentation, centralized security monitoring, and blue team operations.

---

# Table of Contents

- Overview
- Skills Demonstrated
- Lab Environment
- Architecture
- Completed Features
- Validation & Implementation
- Active Directory Deployment
- Wazuh SIEM
- Project Timeline
- Future Expansion
- Key Takeaways

---

# Overview

This project demonstrates the design, deployment, and administration of a secure enterprise-style lab using virtualization and modern security technologies.

The environment currently includes:

- Proxmox VE virtualization
- pfSense firewall
- VLAN segmentation
- Windows Server 2022
- Active Directory Domain Services
- DNS Server
- Wazuh SIEM
- Linux administration
- Windows endpoint monitoring
- Enterprise network architecture

---

# Skills Demonstrated

### Virtualization

- Proxmox VE
- Virtual Machine Deployment
- VirtIO Drivers
- QEMU Guest Agent
- Snapshot Management

### Networking

- pfSense Firewall
- VLAN Configuration
- Inter-VLAN Routing
- Static IP Configuration
- Network Segmentation
- DNS Configuration

### Windows Administration

- Windows Server 2022
- Active Directory Domain Services
- Domain Controller Deployment
- DNS Server
- Windows Administration

### Linux Administration

- Ubuntu Server
- Linux Mint
- SSH
- Package Management

### Security

- Wazuh SIEM
- Endpoint Monitoring
- Windows Agent Deployment
- Linux Agent Deployment
- Firewall Rule Creation

---

# Current Lab Environment

## Infrastructure

- Proxmox VE Hypervisor
- pfSense Community Edition
- Netgear Managed Switch
- VLAN-aware Linux Bridge (vmbr1)

## Management

- Linux Mint Management Workstation
- Firefox Management Station
- SSH Administration

## Security

- Wazuh Manager
- Wazuh Dashboard
- Windows Agent
- Linux Agent

## Windows

- Windows Server 2022
- Active Directory Domain Services
- DNS Server
- Domain Controller (DC01)

## Networking

- VLAN 99 – Management
- VLAN 10 – Clients
- VLAN 20 – Servers

---

# Architecture

```text
                    Internet
                        │
                  Home Router
                        │
                 Proxmox VE Host
                        │
              VLAN Aware Bridge (vmbr1)
                        │
                  pfSense Firewall
          ┌─────────────┼─────────────┐
          │             │             │
     VLAN 99       VLAN 10      VLAN 20
    Management      Clients      Servers
          │                          │
     Linux Mint              Windows Server
                             DC01 (AD/DNS)
                                  │
                           Active Directory
                                  │
                             DNS Services
                                  │
                            Wazuh Manager
```

---

# Completed Features

- Proxmox VE deployment
- Virtual machine provisioning
- VLAN-aware networking
- pfSense firewall deployment
- Inter-VLAN routing
- Linux Mint management workstation
- Ubuntu Server deployment
- Wazuh SIEM deployment
- Windows Server 2022 deployment
- Active Directory installation
- DNS Server installation
- Static IP addressing
- VirtIO driver installation
- QEMU Guest Agent deployment
- Wazuh Windows Agent deployment
- Wazuh Linux Agent deployment

---

# Implementation Journey

## Phase 1 – Network Planning

### Objective

Design the initial enterprise network architecture before deployment.

### Figure 1 – Initial Network Planning

Initial whiteboard sketch created during the planning phase to design the enterprise network architecture. The diagram identifies the Proxmox virtualization host, pfSense firewall, Linux management workstation, VLAN segmentation strategy, and planned server infrastructure prior to implementation.

<p align="center">
  <img src="images/planning/sketch.jpeg" width="650">
</p>

### Outcome

- Initial network topology established
- VLAN layout planned
- Firewall placement identified
- Management network designed

---

## Phase 2 – Proxmox VE Deployment

### Objective

Deploy Proxmox VE as the enterprise virtualization platform responsible for hosting and managing all virtual infrastructure within the homelab.

### Configuration

- Installed Proxmox VE
- Configured local and local-lvm storage
- Created VLAN-aware Linux Bridge (vmbr1)
- Enabled virtualization extensions
- Created virtual machines for:
  - pfSense
  - Linux Mint
  - Wazuh Manager
  - Windows Server 2022 (DC01)

### Validation

- Verified successful VM deployment
- Confirmed resource allocation
- Verified VM startup and shutdown
- Confirmed hypervisor stability

### Figure 2 – Proxmox Virtualization Platform

The Proxmox VE hypervisor serves as the foundation of the homelab, hosting all virtual machines while providing centralized management, storage, networking, and virtualization.

<p align="center">
<img src="images/proxmox/proxmox-dashboard.png" width="900">
</p>

### Figure 3 – VLAN-Aware Linux Bridge Configuration

The Proxmox VLAN-aware Linux bridge (vmbr1) provides virtual switching for all guest machines while supporting IEEE 802.1Q VLAN tagging. This bridge enables pfSense to receive tagged traffic and route communication between management, client, and server networks.

<p align="center">
<img src="images/proxmox/bridge.jpeg" width="650">
</p>

### Outcome

- Enterprise virtualization platform operational
- Multiple virtual machines deployed
- Centralized VM management established
- Foundation prepared for network segmentation and security services

---

## Phase 3 – pfSense Firewall & Network Segmentation

### Objective

Deploy pfSense as the central firewall and router to provide network segmentation, inter-VLAN routing, and secure communication between management, client, and server networks.

### Configuration

- Installed pfSense Community Edition
- Configured WAN and LAN interfaces
- Created Management (VLAN 99)
- Created Client (VLAN 10)
- Created Server (VLAN 20)
- Configured VLAN interfaces
- Implemented inter-VLAN routing
- Created firewall rules for each VLAN
- Configured static IP addressing
- Enabled HTTPS management
- Disabled unnecessary services

### Validation

- Verified VLAN communication
- Confirmed inter-VLAN routing
- Verified firewall rule enforcement
- Validated internet connectivity
- Confirmed management network isolation
- Tested communication between Linux Mint, Wazuh Manager, and Windows Server

### Figure 4 – pfSense Firewall Rules

The pfSense firewall was configured with VLAN-specific firewall policies to control communication between management, client, and server networks while maintaining secure administrative access.

<p align="center">
<img src="images/pfsense/firewall-rules.jpeg" width="850">
</p>

### Figure 5 – Network Connectivity Validation

Network connectivity was validated by testing communication between VLANs and verifying successful routing through the pfSense firewall.

<p align="center">
<img src="images/pfsense/connectivity-validation.jpeg" width="700">
</p>

### Outcome

- Successfully deployed pfSense as the core firewall and router
- Implemented secure VLAN segmentation
- Established controlled inter-VLAN routing
- Verified firewall policy enforcement
- Created a secure network foundation for Active Directory and Wazuh SIEM

---

## Phase 4 – Wazuh SIEM Deployment

### Objective

Deploy Wazuh as the centralized Security Information and Event Management (SIEM) platform to collect, analyze, and monitor security events from Windows and Linux endpoints through a unified management interface.

### Configuration

- Deployed Ubuntu Server 24.04 LTS
- Installed Wazuh Manager
- Installed and configured Wazuh Dashboard
- Installed Wazuh Indexer
- Configured HTTPS dashboard access
- Installed Linux Mint endpoint agent
- Installed Windows Server endpoint agent
- Registered Windows and Linux endpoints with the Wazuh Manager

### Validation

- Verified Wazuh Manager services
- Confirmed Dashboard accessibility
- Verified Linux Mint agent registration
- Verified Windows Server agent registration
- Confirmed secure agent communication
- Validated centralized endpoint monitoring

### Figure 6 – Wazuh Dashboard

The Wazuh dashboard provides centralized visibility into monitored endpoints, security events, and system health.

<p align="center">
<img src="images/wazuh/wazuh-dashboard.png" width="900">
</p>

### Figure 7 – Registered Wazuh Agents

Both Windows Server and Linux Mint successfully enrolled with the Wazuh Manager, demonstrating centralized endpoint monitoring.

<p align="center">
<img src="images/wazuh/wazuh-agents.png" width="850">
</p>

### Figure 8 – Windows Agent Deployment

The Windows Server Wazuh Agent service was verified to be installed and running.

<p align="center">
<img src="images/wazuh/windows-agent-installation.png" width="850">
</p>

### Figure 9 – Linux Management Workstation Validation

The Linux Mint management workstation was validated with an active QEMU Guest Agent and Wazuh Agent.

<p align="center">
<img src="images/wazuh/linux-agent-validation.png" width="750">
</p>

### Outcome

- Successfully deployed enterprise SIEM platform
- Centralized security monitoring established
- Windows and Linux endpoints enrolled
- Secure agent communication verified
- Foundation prepared for future threat detection and log analysis

---

## Phase 5 – Windows Server 2022 Deployment

### Objective

Deploy Windows Server 2022 as the enterprise server platform that will host Active Directory Domain Services and supporting infrastructure.

### Configuration

- Installed Windows Server 2022
- Installed VirtIO drivers
- Installed QEMU Guest Agent
- Configured static IP address
- Renamed server to **DC01**
- Enabled Remote Desktop
- Installed Windows updates

### Validation

Verified server identity and configuration.

```text
hostname

DC01
```

```text
whoami

homelab\administrator
```

### Figure 10 – Server Manager

<p align="center">
<img src="images/windows/server-manager.png" width="900">
</p>

### Figure 11 – Static Network Configuration

<p align="center">
<img src="images/windows/network-settings.png" width="850">
</p>

### Figure 12 – Server Validation

<p align="center">
<img src="images/windows/server-validation.png" width="850">
</p>

### Outcome

- Windows Server successfully deployed
- Enterprise server configuration completed
- Static network configuration verified
- Server prepared for Active Directory deployment

---

## Phase 6 – Active Directory Domain Services

### Objective

Deploy Active Directory Domain Services (AD DS) to provide centralized authentication, DNS, and identity management for the homelab.

### Configuration

- Installed Active Directory Domain Services
- Installed DNS Server
- Created new forest (**homelab.local**)
- Promoted DC01 to Domain Controller
- Configured DNS integration
- Configured SYSVOL and NETLOGON

### Validation

- Verified Domain Controller promotion
- Confirmed Active Directory Users and Computers
- Verified DNS Manager functionality
- Confirmed domain services operational

### Figure 13 – Active Directory Users and Computers

<p align="center">
<img src="images/active-directory/aduc.png" width="900">
</p>

### Figure 14 – DNS Manager

<p align="center">
<img src="images/active-directory/dns-manager.png" width="900">
</p>

### Outcome

- Domain Controller successfully deployed
- Centralized authentication established
- DNS services operational
- Enterprise identity infrastructure completed

---

# Firewall Policy Summary

| Source | Destination | Action | Purpose |
|---------|-------------|--------|---------|
| Users | Servers | Allow | Business communication |
| Clients | Internet | NAT | Internet access |
| Management | All VLANs | Allow | Administrative access |
| Servers | Internet | Restricted | Controlled outbound traffic |

---

# Project Timeline

✅ Phase 1 — Network Planning

✅ Phase 2 — Proxmox VE Deployment

✅ Phase 3 — pfSense Firewall & Network Segmentation

✅ Phase 4 — Wazuh SIEM Deployment

✅ Phase 5 — Windows Server 2022 Deployment

✅ Phase 6 — Active Directory Domain Services

⬜ Phase 7 — Windows 11 Enterprise Client

⬜ Phase 8 — Group Policy

⬜ Phase 9 — Sysmon

⬜ Phase 10 — Splunk Enterprise

⬜ Phase 11 — Attack Simulation & Detection

---

# Future Expansion

Planned enhancements include:

- Windows 11 Enterprise Client
- Domain Join Automation
- Group Policy Objects (GPOs)
- Sysmon Deployment
- Splunk Enterprise
- Windows Event Forwarding (WEF)
- Active Directory User Management
- Organizational Units (OUs)
- Security Groups
- Service Accounts
- Attack Simulation
- Detection Engineering
- SIEM Alert Tuning
- Backup and Recovery Strategy

---

# Key Takeaways

This project demonstrates the design, deployment, and administration of an enterprise-style cybersecurity homelab using industry-standard infrastructure and security technologies.

Key technologies include:

- Proxmox VE
- pfSense
- Ubuntu Server
- Wazuh SIEM
- Windows Server 2022
- Active Directory Domain Services
- DNS
- Windows Administration
- Linux Administration
- Network Segmentation
- Virtualization
- Firewall Administration
- Endpoint Monitoring

The environment will continue to expand with additional enterprise infrastructure, Windows administration, detection engineering, attack simulations, and blue-team security operations to further simulate a production enterprise environment.