# Service Deployment 

This document tracks internal services deployed within the home lab environment, including installation methods, configuration details, and how they are accessed or tested.

---

## Service #1: Nginx Web Server

**Deployed On:** Ubuntu Server  
**IP Address:** 192.168.1.10  
**Port:** 80 (HTTP)  
**Purpose:** Internal web service to simulate hosted applications and test internal HTTPS access


---

### Installation Steps 
  ```
  sudo apt update && sudo apt upgrade -y
  sudo apt install nginx -y
  ```

### Verification 
Checked Nginx service status:
  ```
  sudo systemctl status nginx
  ```
Started and enabled it to run on boot:
  ```
  sudo systemctl start nginx
  sudo systemctl enable nginx
  ```

### Access Tests
| Source VM        | Access Method        | Result                  |
|------------------|----------------------|-------------------------|
| Windows 10       | Browser http://192.168.1.10 | Nginx welcome page loaded |
| Kali Linux       | Browser http://192.168.1.10 | Nginx welcome page loaded |
| Kali Linux       | curl http://192.168.1.10    | Returned Nginx HTML response |

---

### Custom Page Deployed

The default Nginx was replaced with a custom 'index.html' located at: /var/www/html/index.html.
The page includes basic server information and confirms internal web hosting. 

---

## Future Enhancements 

- Create firewall rules to restrict HTTP access by IP or VLAN
- add HTTPS with self-signed or internal certificate 
