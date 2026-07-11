# Site-to-Site VPN using MikroTik & WireGuard

## 📌 Project Overview
This project demonstrates a secure, highly reliable Site-to-Site VPN architecture designed for a retail company with multiple branches. The goal was to securely connect remote branches to a central accounting system (Al-Khawarizmi Server) over port `1433`.

## 🛑 The Challenge (Double NAT & Security)
Prior to this implementation, the client relied on basic Port Forwarding directly on the ISP modems. This approach caused severe instability and disconnections due to:
- **Double NAT / CGNAT** issues causing asymmetric routing.
- Security vulnerabilities from exposing the main SQL database port directly to the public internet via DDNS.

## 💡 The Solution
To resolve the routing conflicts and secure the database traffic, I implemented the following infrastructure:
1. **MikroTik Routers Deployment:** Placed MikroTik routers behind the ISP modems at the Main HQ and all remote branches.
2. **WireGuard VPN Tunnel:** Configured a lightweight, encrypted WireGuard tunnel bypassing the unreliable ISP public routing.
3. **Advanced NAT Routing:** Configured `dst-nat`, `src-nat` (Masquerade), and Hairpin NAT rules to ensure traffic from remote branches accurately reaches the local server without dropping the TCP handshake.

## 🗺️ Network Topology
*The diagram below illustrates the physical ISP connections, the WireGuard tunnels, and the flow of traffic to the internal core switch and servers.*

![Network Topology](Bin-Mahri%20Diagram.drawio.png)

## 🛠️ Technologies Used
- **Hardware:** MikroTik Routers, Core Switches
- **Protocols:** WireGuard VPN, TCP/IP
- **Concepts:** Port Forwarding, DMZ, Double NAT bypass, Hairpin NAT, Firewall Filter Rules
