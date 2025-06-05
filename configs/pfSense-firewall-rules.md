# pfSense Firewall Rules

**Author:** Bosco Lasrado
**Lab Setup:** Home Lab - pfSense with 3 internal VMs
**Objective:** Simulate basic traffic filtering and rule testing in a real-world small office network. 

---

## Test Rule 1: Block ICMP (ping) from Kali to Ubuntu 

### Rule Purpose 
To simulate basic internet network segmentation by preventing the "attacker" VM (Kali) from pinging the internal server (Ubuntu).

---

### Rule Details 


| Setting        | Value                       |
|----------------|-----------------------------|
| **Action**     | Block                       |
| **Interface**  | LAN                         |
| **Protocol**   | ICMP                        |
| **Source**     | 192.168.1.102 (Kali)        |
| **Destination**| 192.168.1.10 (Ubuntu)       |
| **Log**        | Enabled (for audit purposes)|

---

### 🧪 Steps to Apply in pfSense

1. Navigate to **Firewall > Rules > LAN**
2. Click **Add** (up arrow – add to top of list)
3. Set:
   - **Action**: Block
   - **Interface**: LAN
   - **Protocol**: ICMP
   - **Source**: `Single host or alias` → `192.168.1.102`
   - **Destination**: `Single host or alias` → `192.168.1.10`
4. ✅ Check **Log packets that are handled by this rule**
5. Click **Save**, then **Apply Changes**
