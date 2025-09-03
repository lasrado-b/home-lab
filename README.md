# Home Lab: IT Networking & Security Simulation

This is a self-directed home lab built to simulate a small office IT environment. The goal is to strengthen real-world skills in networking, system administration, and cybersecurity using open-source tools and virtual machines. It complements my formal certifications and customer support experience as I transition into technical IT roles.

---

## About Me

I'm Bosco Lasrado, an IT Support and Customer Experience Professional with 5+ years in customer-facing roles and recent hands-on technical training. Certified in CompTIA Network+ and Google IT Support, I'm building this home lab to sharpen skills and demonstrate initiative to prospective employers.

---

## Lab Environment

| VM Name       | OS             | Role               | IP Address      | Hostname       |
|---------------|----------------|--------------------|------------------|----------------|
| pfSense        | pfSense CE     | Firewall & Router  | 192.168.1.1      | pfsense         |
| Win10-User     | Windows 10     | Workstation        | DHCP/static     | win10-user      |
| Ubuntu-Server  | Ubuntu Server  | Internal Services  | 192.168.1.10     | blues-server     |
| Kali-Attacker  | Kali Linux     | Pentesting/Testing | DHCP/static     | blues-attack    |

---

## Project Goals

- Simulate a real-world small office IT infrastructure
- Implement firewall rules and VLAN segmentation with pfSense
- Practice system administration tasks across Linux and Windows
- Set up internal services (file sharing, web, DNS, logging)
- Test and harden systems through red-team/blue-team exercises

---

## Current Progress

- [x] Deployed pfSense with LAN/WAN configuration
- [x] Installed and configured Ubuntu Server with static IP
- [x] Created and configured Kali Linux for testing
- [x] Verified full network connectivity between VMs
- [ ] Enabled SSH access to Ubuntu Server
- [ ] Created basic pfSense firewall rules
- [ ] Documented network layout and rules

---

## Firewall Configuration

- Configured pfSense firewall rules to block unauthorized traffic.
- Blocked all traffic from Kali subnet (192.168.2.0/24) to the Ubuntu server (192.168.1.10).
- Verified the block by testing ICMP (ping) and confirmed 100% packet loss from Kali to Ubuntu.
- Kali retains network access to other devices (e.g., pfSense, Windows VM, external internet) confirming proper segmentation.

---

## Tools and Technologies Used

- VirtualBox
- pfSense CE
- Ubuntu Server 22.04
- Windows 10
- Kali Linux
- OpenSSH
- Netplan (static IP)
- ICMP/DNS/NAT troubleshooting
- Markdown (for documentation)

---

# Active Directory Expansion

This document outlines the addition of a Microsoft Active Directory (AD) environment into the **Home Lab**. The goal is to simulate a real-world enterprise setup, practice domain management, and showcase skills relevant to IT, system administration, and cybersecurity roles.

---

## 🔹 Architecture Overview
- **Domain Controller (DC):** Windows Server 2022 (trial)
- **Domain Name:** `homelab.local`
- **Client VM:** Windows 10/11 joined to the domain
- **Optional:** Ubuntu client joined via LDAP/SSSD for Linux integration
- **Network Segmentation:** DC in **server VLAN**, clients in **workstation VLAN** (controlled via pfSense)

---

## 🔹 VM Requirements
**Windows Server 2022 (Domain Controller)**
- 2 vCPUs  
- 4–6 GB RAM  
- 60 GB storage  
- Static IP in *Server subnet*  

**Windows 10/11 Client**
- 2 vCPUs  
- 4 GB RAM  
- 40 GB storage  
- DHCP in *Workstation subnet*  

---

## 🔹 Setup Steps

### 1. Install Windows Server 2022
- Use Microsoft’s evaluation ISO.  
- Select **Desktop Experience** during installation.  
- Configure a static IP (example: `192.168.10.10`).  

### 2. Install Active Directory Domain Services (AD DS)
- Open **Server Manager** → **Add Roles and Features** → enable **AD DS**.  
- Promote to Domain Controller.  
- Create a new forest: `homelab.local`.  
- Install DNS role during promotion.  

### 3. Configure Organizational Units (OUs)
- Create the following structure in **Active Directory Users and Computers**:  
  - `OU=Users`  
  - `OU=Computers`  
  - `OU=Groups`  

### 4. Create Test Accounts
- User: `bosco.lasrado` → Domain Admin.  
- User: `mendes.test` → Standard User.  
- Groups: `IT_Staff`, `HR_Staff`.  

### 5. Join Windows Client to Domain
- On Windows 10/11, point DNS to the DC (`192.168.10.10`).  
- Join domain: `homelab.local`.  
- Log in as `mendes.test`.  

### 6. Apply Group Policy (GPO)
Examples to practice:
- Enforce strong password policies.  
- Redirect Documents folder to a network share.  
- Map a network drive automatically.  
- Disable Control Panel for standard users.  

### 7. Integration Scenarios (Optional)
- **pfSense:** Use AD for VPN authentication.  
- **Nextcloud:** Configure LDAP/AD login.  
- **Linux Client:** Join Ubuntu to AD with `realmd` + `sssd`.  

---

## 🔹 Real-World Scenarios to Practice
- **User Onboarding:** Create new users, assign groups, test access.  
- **Access Control:** Restrict HR files to `HR_Staff` only.  
- **Policy Enforcement:** Push software restrictions or desktop settings via GPO.  
- **Troubleshooting:** Apply GPO → run `gpupdate /force` → verify with `rsop.msc`.  
- **Helpdesk Simulation:** Reset locked-out passwords, expire accounts, disable users.  

---

## 🔹 Documentation to Include
- Screenshots:  
  - AD DS installation  
  - Domain join confirmation  
  - GPO applied on client  
- Network diagram showing AD’s place in the lab  
- Notes on issues + fixes (for troubleshooting documentation)  

---

## 🔹 Next Steps
- Add a **second Domain Controller** for redundancy (optional advanced exercise).  
- Explore **Group Policy Preferences** (drive mappings, registry changes).  
- Practice **AD security hardening** (audit policies, Kerberos, account lockout thresholds).  

---

## Network Diagram

![Network Diagram](diagrams/network-topology-updated.drawio.png)

## Repo Structure
```
/README.md <- Project overview, goals, setup
/checklist.md <- Weekly or project-based to-do list
/configs/ <- Config files
├── netplan-static-ip.yaml
├── pfSense-firewall-rules.md
/logs/ <- Test results, command outputs, and troubleshooting notes
├── connectivity-tests.md
└── troubleshooting-notes.md
/diagrams/ <- Network diagrams
└── network-topology.drawio
```
