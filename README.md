# Cisco Packet Tracer Networking Labs

A collection of progressively advanced networking labs built in Cisco Packet Tracer while studying Computer Networking.

## Lab Progression

| Lab Project | Concepts Covered | Date Completed | Topology |
| :--- | :--- | :--- | :--- |
| **Basic LAN** | Static IP, Layer 2 Switching | June 2026 | [View](images/basic-lan-topology.png) |
| **Secure SOHO** | Wireless, DHCP | June 2026 | [View](images/secure-soho-topology.png) |
| **Enterprise Gateway** | Default Gateways, L3 Routing | June 2026 | [View](images/enterprise-gateway-topology.png) |
| **Enterprise LAN/WAN** | ISP Connectivity, Public Routing | June 2026 | [View](images/enterprise-lan-wan-topology.png) |

---

## Lab Spotlight: Enterprise LAN/WAN

### Overview
This project expanded the local corporate network into a routed WAN environment, establishing a default gateway to bridge private internal traffic to the public internet.

### Technologies Used
- Cisco Packet Tracer / ISR 4331 Router / Catalyst 2960 Switch
- IPv4 Addressing & Subnetting
- Static Routing (Gateway of Last Resort)
- DHCP Services
- WAN Connectivity (Transit Subnets)

### Troubleshooting Log
* **Issue:** Ping request timed out when testing connectivity to the ISP.
* **Root Cause:** Asymmetric routing; the ISP router lacked a return route for the `192.168.1.0/24` internal network.
* **Resolution:** Configured a static route (`ip route 192.168.1.0 255.255.255.0 10.0.0.2`) on the ISP router pointing back to the edge gateway.

### Verification

#### EDGE-ROUTER
* **Interface Status:** ![Interface Brief](images/edge-router-brief.png)
* **Routing Table:** ![Routing Table](images/edge-router-route.png)

#### ISP-ROUTER
* **Interface Status:** ![Interface Brief](images/isp-router-brief.png)
* **Routing Table:** ![Routing Table](images/isp-router-route.png)

---

## Planned Labs
- [x] Basic LAN
- [x] Secure SOHO
- [x] Enterprise Gateway
- [x] Enterprise LAN/WAN
- [ ] VLAN Segmentation
- [ ] Router-on-a-Stick
- [ ] ACLs (Access Control Lists)
- [ ] NAT/PAT
- [ ] OSPF Routing
- [ ] Port Security
