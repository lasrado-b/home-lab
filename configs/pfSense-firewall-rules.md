# pfSense Firewall Rules

**Author:** Bosco Lasrado

**Lab Setup:** Home Lab - pfSense with 3 internal VMs

**Objective:** Simulate basic traffic filtering and rule testing in a real-world small office network. 

## Firewall Rules Summary

| Rule | Purpose                               | Source               | Destination        | Protocol |
|------|---------------------------------------|----------------------|--------------------|----------|
| 1    | Block ICMP (ping) from Kali to Ubuntu | 192.168.1.102 (Kali) | 192.168.1.10       | ICMP     |
| 2    | Block HTTP access from Kali to Ubuntu | 192.168.1.102 (Kali) | 192.168.1.10       | TCP 80   |
| 3    | Block all traffic from Kali subnet    | 192.168.2.0/24       | 192.168.1.10       | Any      |

## Firewall Evolution: Phased Approach

This firewall setup was built in **progressive phases** to demonstrate how security policies can evolve from simple, protocol-specific rules to broader, scalable subnet-based segmentation.

### Phase 1: Protocol-Specific Blocking
- **Test Rule 1:** Blocked ICMP (ping) from Kali to Ubuntu to prevent basic network discovery.
- **Test Rule 2:** Blocked HTTP (port 80) access from Kali to Ubuntu to restrict web service exposure.

These initial rules provided targeted protections and were useful for practicing specific firewall configurations and testing granular controls.

### Phase 2: Subnet-Wide Isolation
- **Test Rule 3:** Implemented a more scalable, comprehensive rule that blocks **all traffic from the entire Kali subnet (192.168.2.0/24) to Ubuntu.**

This rule phased out the need for the earlier, protocol-specific blocks by fully segmenting the attacker network from the internal server.

---

## Phase 1: Protocol-Specific Blocking
### Test Rule 1: Block ICMP (ping) from Kali to Ubuntu
#### Rule Purpose 
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
  ```

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
  ```

**Notes:**
- This rule simulates internal segmentation between sensitive services (Ubuntu) and untrusted endpoints (Kali).
- ICMP blocking is a basic but effective test before implementing port-specific filtering.

### Test Rule 2: Block HTTP Access to Web Server from Kali
#### Rule Purpose 
Restrict port 80 access to Ubuntu web server (192.168.1.10) only to approved devices (eg. Windows)

### Rule Details

| Setting        | Value                       |
|----------------|-----------------------------|
| **Action**     | Block                       |
| **Protocol**   | TCP                         |
| **Port**       | 80 (HTTP)                   |
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
   - **Protocol**: TCP
   - **Port**: 80
   - **Source**: `Single host or alias` → `192.168.1.102`
   - **Destination**: `Single host or alias` → `192.168.1.10`
4. Check **Log packets that are handled by this rule**
5. Click **Save**, then **Apply Changes**

### Test Results
- [x] Kali denied access to internal web service
- [x] Windows still able to load custom dashboard

---

## Phase 2: Subnet-Wide Isolation
### Test Rule 3: Block All Traffic from Kali Subnet to Ubuntu
#### Rule Purpose
This rule was introduced as part of the next stage of the lab to simplify and scale security controls by isolating the entire Kali subnet.

### Rule Details

| Setting        | Value                          |
|----------------|--------------------------------|
| **Action**     | Block                          |
| **Interface**  | LAN                            |
| **Protocol**   | Any                            |
| **Source**     | 192.168.2.0/24 (Kali Subnet)   |
| **Destination**| 192.168.1.10 (Ubuntu Server)   |
| **Log**        | Enabled (for audit purposes)   |

## Test Results
- [x] Ping from Kali to Ubuntu: 100% packet loss (Blocked)
- [x] SSH from Kali to Ubuntu: Not tested, but should also be blocked
- [x] Kali can still ping pfSense (192.168.1.1) and other devices
- [x] Kali can still access the internet

## Notes
- Rule is placed **above the default allow LAN rule** to ensure it takes precedence.
- Logging is enabled for this rule to support auditing. Can be disabled to save log space if required.
