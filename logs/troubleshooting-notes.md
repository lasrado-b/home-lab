### 🛑 Issue: Cannot Ping Windows VM from Other VMs (Ubuntu/Kali)

**Symptoms:**
- Windows VM (192.168.1.100) could ping all other devices.
- Ubuntu and Kali could ping each other and pfSense, but **not Windows**.
- All devices had internet access and correct IPs.

**Root Cause:**
- By default, Windows Firewall blocks inbound ICMP Echo requests (ping).

**Fix (via Command Line):**
Open **Command Prompt as Administrator** and run:
```
netsh advfirewall firewall add rule name="Allow ICMPv4-In" protocol=icmpv4:8,any dir=in action=allow
