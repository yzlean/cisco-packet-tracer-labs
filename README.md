# Cisco Packet Tracer Networking Labs

A collection of progressively advanced networking labs built in Cisco Packet Tracer while studying Computer Networking.

## Lab Progression

| Lab Project | Concepts Covered | Date Completed | Topology |
| :--- | :--- | :--- | :--- |
| **Basic LAN** | Static IP, Layer 2 Switching | June 2026 | [View](images/basic-lan-topology.png) |
| **Secure SOHO** | Wireless, DHCP | June 2026 | [View](images/secure-soho-topology.png) |
| **Enterprise Gateway** | Default Gateways, L3 Routing | June 2026 | [View](images/enterprise-gateway-topology.png) |
| **Enterprise LAN/WAN** | ISP Connectivity, Public Routing | June 2026 | [View](images/enterprise-lan-wan-topology.png) |
| **VLAN Segmentation** | Broadcast Domains, L2 Isolation | June 2026 | [View](images/vlan-segmentation-topology.png) |

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
  *Confirmed that all local and WAN interfaces are operational and correctly addressed.*
* **Routing Table:** ![Routing Table](images/edge-router-route.png)
  *Confirmed that the router contains a default route (`S*`) pointing to the ISP router, establishing the path for outgoing traffic.*

#### ISP-ROUTER
* **Interface Status:** ![Interface Brief](images/isp-router-brief.png)
  *Confirmed that the ISP-facing and transit interfaces are active and communicating.*
* **Routing Table:** ![Routing Table](images/isp-router-route.png)
  *Confirmed that the ISP router contains a static return route to the internal `192.168.1.0/24` network, ensuring bidirectional traffic flow.*

---

## Lab Spotlight: Department Segmentation with VLANs

### Overview
This project addresses a flat corporate network domain by engineering Layer 2 network segmentation. By creating dedicated virtual local area networks (VLANs), department broadcast traffic is completely contained, mitigating security vulnerabilities and performance bottlenecks.

### Technologies Used
- Cisco Catalyst 2960 Layer 2 Switch
- Logical Segmentation (802.1Q VLAN Mapping)
- Broadcast Domain Isolation

### Troubleshooting Log
* **Issue 1: CLI Configuration Fails with "Invalid input detected" Marker**
  * **Root Cause:** Attempted to execute the `configure terminal` command while the switch CLI was running in restricted *User Exec Mode* (`Switch>`). 
  * **Resolution:** Elevated privileges by executing the `enable` command to enter *Privileged Exec Mode* (`Switch#`), unlocking global configuration capabilities.

* **Issue 2: VLAN Mappings Failed to Isolate Intended Devices**
  * **Root Cause:** Misalignment between the assumed network topology design and actual physical layer cabling connections. The IT laptop was physically patched into interface `Fa0/3` and the Company Server into `Fa0/1`, mismatching the initial configuration script.
  * **Resolution:** Executed `show mac address-table` on the switch CLI after generating host traffic to definitively map active MAC addresses to physical ingress ports. Updated the running configuration to bind interfaces `Fa0/1`, `Fa0/2`, and `Fa0/3` to their correct respective VLAN domains (10, 20, and 30) and updated network topology documentation for structural accuracy.

### Verification

#### CORE-SWITCH
* **VLAN Database Initialization:** ![VLAN Brief Initial](images/vlan-brief.png)
  *Confirmed the successful creation and activation of VLANs 10, 20, 30, and 99 within the switch database before port allocation.*
* **Port Assignments:** ![VLAN Assignments](images/vlan-assignments.png)
  *Confirmed that FastEthernet 0/1 is actively assigned to the HR VLAN (10) and FastEthernet 0/2 is actively assigned to the IT VLAN (20).*

### Testing Results (Layer 2 Isolation)
* **Cross-VLAN Drop Test:** ![Failed Ping](images/ping-fail.png)
  *Attempted a ping from HR-PC (192.168.10.2) to IT-PC (192.168.20.2). The ping timed out completely, validating that Layer 2 isolation is operating perfectly and devices cannot communicate across broadcast domains without a Layer 3 routing engine.*

---

## Planned Labs
- [x] Basic LAN
- [x] Secure SOHO
- [x] Enterprise Gateway
- [x] Enterprise LAN/WAN
- [x] VLAN Segmentation
- [ ] Router-on-a-Stick (Inter-VLAN Routing)
- [ ] ACLs (Access Control Lists)
- [ ] NAT/PAT
- [ ] OSPF Routing
- [ ] Port Security
