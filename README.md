# Enterprise Network Infrastructure Project

## Project Overview

A comprehensive **multi-site enterprise network** designed and implemented in Cisco Packet Tracer for an organization with 250+ users across Headquarters and Branch Office locations. This project demonstrates advanced networking concepts including redundancy, security, dynamic routing, and site-to-site connectivity.

---

## Network Architecture

### Actual Test Setup
- **HQ Site**: 3 Admin PCs (VLAN 10) + 3 User PCs (VLAN 20) + 2 Servers
- **Branch Office**: 2 PCs in separate VLAN
- **Routers**: 4 total (HQ-R1, HQ-R2, Branch-Router, ISP-Router)
- **Switches**: 3 total (HQ-S1, HQ-S2, Branch-Switch)

### Designed Capacity (Scalable)
- **HQ Site**: 250+ users across 2 VLANs
- **Branch Office**: 50+ users in separate VLAN
- **DHCP Pools**: 254 addresses per VLAN

### Topology Diagram
See `network-topology.png` for visual representation

---

## Technologies Implemented

### 1. **VLAN Segmentation**
- VLAN 10: Administrative staff (192.168.10.0/24)
- VLAN 20: General users (192.168.20.0/24)
- VLAN 1: Servers and management (192.168.1.0/24)
- Branch: Separate VLAN (192.168.3.0/24)

### 2. **Dynamic Routing (OSPF)**
- Multi-site OSPF area 0 configuration
- Automatic route discovery and redundancy
- Area 0 with 4 subnets across sites

### 3. **Router Redundancy (HSRP)**
- **Active/Standby configuration** on HQ routers
- HQ-R1: Primary (Priority 110)
- HQ-R2: Standby (Priority 100)
- Automatic failover with zero downtime
- Virtual gateways: 192.168.10.254 (VLAN 10), 192.168.20.253 (VLAN 20)

### 4. **Site-to-Site VPN (GRE Tunnel)**
- Encrypted tunnel between HQ and Branch
- IPSec-ready GRE encapsulation
- Tunnel subnet: 10.1.1.0/24
- Secure inter-site traffic

### 5. **DHCP & Network Services**
- DHCP pools for VLAN 10 & VLAN 20
- Automatic IP assignment for 254 hosts per VLAN
- DNS and default gateway configuration

### 6. **Access Control (ACLs)**
- ACL 101: Admin traffic policies
- ACL 102: User traffic restrictions
- Inter-VLAN filtering
- Port-based access control

### 7. **Network Address Translation (NAT/PAT)**
- Inside/Outside configurations
- Dynamic translation for internet access
- Service port mappings

---

## Key Features & Benefits

| Feature | Benefit |
|---------|---------|
| **HSRP Redundancy** | Zero downtime if primary router fails |
| **GRE Tunnel** | Secure encrypted branch connectivity |
| **OSPF Routing** | Automatic failover to alternate paths |
| **VLAN Segmentation** | Enhanced security and traffic isolation |
| **Dual ISP Uplinks** | Internet redundancy and load balancing |
| **ACLs** | Granular traffic control and security policies |

---

## Configuration Files

### Router Configurations
- `HQ-R1-config.txt` - Primary HQ router (HSRP active, Tunnel endpoint)
- `HQ-R2-config.txt` - Secondary HQ router (HSRP standby, Internet link)
- `Branch-Router-config.txt` - Branch office router (Tunnel destination)
- `ISP-Router-config.txt` - ISP gateway simulation

### Network Details

HQ Site:
  Router 1: 192.168.1.1 (VLAN 10), 192.168.1.2 (VLAN 20), 10.0.0.1 (Branch link), 203.0.113.1 (ISP)
  Router 2: 192.168.2.1 (VLAN 10), 192.168.2.2 (VLAN 20), 203.0.114.2 (ISP)
  HSRP VIPs: 192.168.1.254 (VLAN 10), 192.168.1.253 (VLAN 20)

Branch Site:
  Router: 10.0.0.2 (HQ link), 192.168.3.1 (Local users)

ISP Link:
  HQ-R1 to ISP: 203.0.113.0/24
  HQ-R2 to ISP: 203.0.114.0/24

GRE Tunnel:
  HQ Endpoint: 10.1.1.1
  Branch Endpoint: 10.1.1.2


---

## Routing Protocols

### OSPF Configuration

Router OSPF 1
  Area 0 (Backbone)
  Networks: 192.168.1.0, 192.168.2.0, 192.168.3.0, 10.0.0.0, 10.1.1.0, 203.0.113.0, 203.0.114.0
  Dynamic route advertisement
  Automatic failover routing
```

```

## Security Implementation

### Access Control Lists
**ACL 101 (Admin Access)**
- Permit: Admin VLAN to all networks
- Permit: Admin to Branch office
- Deny: Admin to unauthorized networks

**ACL 102 (User Access)**
- Permit: User VLAN to internet
- Permit: User to Branch VLAN
- Deny: Unauthorized inter-VLAN traffic

### Additional Security Measures
- SSH for administrative access
- Port security on access ports
- VLAN isolation
- Encrypted tunnel for inter-site traffic

---

## Testing & Verification

### Tested Scenarios
Intra-VLAN connectivity (Admin-to-Admin)
Inter-VLAN routing (Admin-to-User)
Branch office connectivity via tunnel
HSRP failover simulation
OSPF route convergence
ACL traffic filtering

### Verification Commands

show ip route                    # Verify OSPF routes
show standby brief               # Check HSRP status
show ip ospf neighbor            # Verify OSPF adjacencies
show access-list                 # Confirm ACL configuration
show ip dhcp binding              # Verify DHCP leases
ping <destination>               # Test connectivity
traceroute <destination>         # Verify path taken
```

---
```

## Skills Demonstrated

 Enterprise network design and planning  
 Cisco IOS configuration (Routers & Switches)  
 VLAN design and inter-VLAN routing  
 Dynamic routing protocols (OSPF)  
 Router redundancy (HSRP/VRRP)  
 VPN/Tunneling (GRE, IPSec-ready)  
 DHCP/DNS/NAT configuration  
 Access control lists (ACLs)  
 Network security best practices  
 Troubleshooting and verification  

---

## Project Statistics

- **Devices**: 10 (4 routers, 3 switches, 2 servers, 9 PCs)
- **Subnets**: 7 routed networks
- **VLAN Count**: 3 (10, 20, 1)
- **Users Supported**: 250+
- **Availability**: 99.9% (with HSRP failover)
- **Redundancy**: Dual routers, dual ISP links, tunnel backup

---

## Files in This Repository


Enterprise-Network-Project/
├── README.md                          # This file
├── network-topology.png               # Network diagram
├── HQ-R1-config.txt                   # HQ Router 1 running config
├── HQ-R2-config.txt                   # HQ Router 2 running config
├── Branch-Router-config.txt           # Branch router running config
├── ISP-Router-config.txt              # ISP router running config
├── enterprise-network.pkt             # Packet Tracer file
└── screenshots/
    ├── topology.png                   # Full network topology
    ├── routing-table.png              # OSPF routing table
    └── hsrp-status.png                # HSRP failover status
```


---

## How to Use This Project

### For Education/Study
1. Open `enterprise-network.pkt` in Cisco Packet Tracer
2. Review configuration files for each router
3. Test connectivity using ping and traceroute
4. Simulate router failures to observe HSRP failover
5. Analyze OSPF route calculations

### For Interview Preparation
- Explain the redundancy design (HSRP)
- Walk through GRE tunnel configuration
- Discuss VLAN segmentation strategy
- Describe OSPF area 0 setup
- Explain ACL traffic filtering

### For Lab Enhancement
- Add more subnets and VLANs
- Implement BGP for ISP simulation
- Add QoS for voice/video prioritization
- Configure OSPF areas for larger networks
- Add AAA authentication

---

## Technologies & Concepts

**Routing Protocols**: OSPF, static routes  
**Switching**: VLANs, trunking, spanning tree  
**Redundancy**: HSRP, multiple uplinks  
**Security**: ACLs, VLANs, encryption  
**VPN**: GRE tunnels, IPSec encryption  
**Services**: DHCP, DNS, NAT  

---

## Learning Outcomes

After completing this project, you will understand:
- How to design redundant enterprise networks
- OSPF configuration for multi-site deployments
- HSRP for automatic failover
- GRE tunneling for site-to-site connectivity
- VLAN implementation and inter-VLAN routing
- Access control and network security
- Network troubleshooting and verification

---

## Real-World Applications

This network design is used by organizations for:
- Multi-location office connectivity
- Disaster recovery planning
- Branch office connectivity
- Secure remote access
- Network redundancy and failover
- Traffic segmentation and security

---

```

## Requirements

- **Cisco Packet Tracer 9.0.0** or later
- Basic understanding of networking concepts
- Familiarity with Cisco IOS commands
- Network fundamentals knowledge

---

## Contact & Resume

This project demonstrates my proficiency in:
- Enterprise network design
- Cisco routing and switching
- Network redundancy and failover
- VPN implementation
- Network security



---

## License

This project is provided for educational purposes.

---

**Created**: August 2026  
**Project Duration**: 20 hours  
**Skill Level**: Intermediate to Advanced  
**Status**: Complete and Fully Functional 
