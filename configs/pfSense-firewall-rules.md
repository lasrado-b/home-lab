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

### Steps to Apply in pfSense

1. Navigate to **Firewall > Rules > LAN**
2. Click **Add** (up arrow – add to top of list)
3. Set:
   - **Action**: Block
   - **Interface**: LAN
   - **Protocol**: ICMP
   - **Source**: `Single host or alias` → `192.168.1.102`
   - **Destination**: `Single host or alias` → `192.168.1.10`
4. Check **Log packets that are handled by this rule**
5. Click **Save**, then **Apply Changes**

---

### Test Result

- From Kali:
  ```
  PING 192.168.1.10 (192.168.1.10) 56(84) bytes of data.
  From 192.168.1.102 icmp_seq=1 Destination Host Unreachable
  ping: sendmsg: No route to host

- From Ubuntu:
 ```
 PING 192.168.1.102 (192.168.1.102) 56(84) bytes of data.
 64 bytes from 192.168.1.102: icmp_seq=1 ttl=64 time=0.019 ms
 64 bytes from 192.168.1.102: icmp_seq=2 ttl=64 time=0.032 ms
 64 bytes from 192.168.1.102: icmp_seq=3 ttl=64 time=0.039 ms
 ^C
 --- 192.168.1.102 ping statistics ---
 3 packets transmitted, 3 received, 0% packet loss, time 2027ms
 rtt min/avg/max/mdev = 0.019/0.030/0.039/0.008 ms
 
