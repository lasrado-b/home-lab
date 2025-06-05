# Virtual Machine Overview

This file documents the current virtual machines deployed in the home lab environment. It includes details like operating system, IP address, hostname, and each VM's role in the network.

---

### VM Summary Table

| VM Name       | OS             | Hostname       | IP Address       | Role / Purpose                   |
|---------------|----------------|----------------|------------------|----------------------------------|
| pfSense        | pfSense CE     | pfsense         | 192.168.1.1      | Router / Firewall (LAN Gateway)  |
| Ubuntu Server  | Ubuntu 22.04   | ubuntu-srv      | 192.168.1.10     | Internal server (SSH, Pi-hole)   |
| Windows 10     | Windows 10     | win10-user      | 192.168.1.100    | Workstation (simulated employee) |
| Kali Linux     | Kali Linux     | kali-attack     | 192.168.1.102    | Attacker / penetration testing   |

---

## Notes

- pfSense handles DHCP and NAT for LAN devices
- Ubuntu uses a static IP configured via Netplan
- Windows and Kali are currently using DHCP
- All hostnames have been set and verified
- pfSense firewall rules are applied to manage internal traffic

---

## Planned Expansions

- Add internal services (Pi-hole, file server, or web server)
- Introduce VLAN segmentation or a DMZ network
- Document MAC addresses or add VM snapshots
