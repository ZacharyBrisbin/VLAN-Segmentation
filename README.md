# 🏗 VLAN Segmentation Lab – Enterprise Network Simulation
## 📌 Overview

This lab transforms a flat virtual network into a segmented enterprise-style architecture using VLAN-like segmentation inside VirtualBox and pfSense.

It implements:

- Network segmentation
- Inter-VLAN routing
- Firewall-based traffic control
- Domain integration across isolated subnets
- Designed for hands-on experience with enterprise network security and infrastructure design.

# 🎯 Objectives

- Create isolated internal network segments
- Configure pfSense as a layer 3 gateway
- Enable controlled inter-VLAN communication
- Restrict traffic using firewall policies
- Support Active Directory communication across subnets
- Implement proper DNS and DHCP configuration

# 🏗 Lab Architecture
Virtual Networks
Network	Purpose	Subnet
VLAN10	Client Devices	192.168.10.0/24
VLAN20	Servers / Domain Controller	192.168.20.0/24
VLAN30	Management	192.168.30.0/24
Virtual Machine Roles
VM	Network	IP
pfSense	WAN + VLAN10 + VLAN20 + VLAN30	Gateway for all subnets
Domain Controller	VLAN20	192.168.20.10
Client Machine	VLAN10	DHCP / Static
# 🔥 Network Flow
```
Client (VLAN10)
      ↓
pfSense (Routing + Firewall)
      ↓
Domain Controller (VLAN20)
      ↓
Internet via WAN
```

Traffic between VLANs is filtered by firewall rules.

# ⚙ Configuration Steps (High Level)
## 1. VirtualBox Setup

Create Internal Networks:

- VLAN10
- VLAN20
- VLAN30

Assign network adapters:

pfSense → One adapter per VLAN + WAN

VMs → Attach to appropriate VLAN

## 2. pfSense Configuration

Assign interfaces to VLAN networks

Enable each interface


Assign static IPs:
```
- VLAN10 → 192.168.10.1
- VLAN20 → 192.168.20.1
- VLAN30 → 192.168.30.1
```

Enable DHCP for client subnet

Configure NAT for outbound internet

Create firewall rules:

Allow required AD traffic

Allow DNS

Allow TCP/UDP between VLAN10 → VLAN20

Block unrestricted traffic

## 3. Domain Controller Configuration

Static IP: 192.168.20.10

Gateway: 192.168.20.1

DNS: Self (192.168.20.10)

## Verify:
- DNS resolution
- AD services functioning

## 4. Client Configuration

- Attach to VLAN10
- Use DHCP (recommended)
- DNS must point to: 192.168.20.10
  
## Test:

- Ping gateway
- Resolve domain
- Join domain

# ✅ Validation Checklist

Your lab is successful when:

✔ Client receives IP from VLAN10

✔ Client resolves domain name

✔ Client can join domain

✔ Inter-VLAN communication works only as permitted

✔ Internet access works via pfSense

✔ Firewall blocks unauthorized traffic

# 🔐 Security Controls Implemented

## Network segmentation

Policy-based firewall filtering

Restricted inter-VLAN access

Controlled DNS resolution

Controlled domain access

# 🚨 Troubleshooting

If connectivity fails:
- Verify internal network names match exactly
- Confirm interfaces are enabled in pfSense
- Check firewall rule order
- Review firewall logs for blocked traffic
- Confirm DNS points to the domain controller

# 📈 Skills Demonstrated

- VLAN architecture (simulated)
- Firewall policy design
- Routing configuration
- Active Directory networking
- DHCP + DNS integration
- Enterprise network troubleshooting
