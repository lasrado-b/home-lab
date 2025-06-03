# Weekly Home Lab Checklist (Goal: Complete by Friday)

## Infrastructure Setup
- [x] Set static IP on Ubuntu Server via Netplan
- [x] Confirm internet and DNS work from Ubuntu
- [ ] Set hostname for all VMs (Ubuntu, Kali, Windows)
- [ ] Ensure all VMs can ping each other and pfSense

## Remote Access
- [x] Install and enable OpenSSH on Ubuntu Server
- [x] Test SSH access from Kali to Ubuntu

## Firewall Configuration
- [ ] Create a pfSense rule to block ICMP (ping) from Kali to Ubuntu
- [ ] Test and log blocked traffic
- [ ] Document the rule's purpose and behavior

## Documentation
- [ ] Create `README.md` in GitHub repo
- [ ] Add current network diagram (hand-drawn or draw.io)
- [ ] Document static IPs and hostnames for each VM
