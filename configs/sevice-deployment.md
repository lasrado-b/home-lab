# Service Deployment 

This document tracks internal services deployed within the home lab environment, including installation methods, configuration details, and how they are accessed or tested.

---

## Service #1: Nginx Web Server

**Deployed On** Ubuntu Server
**IP Address** 192.168.1.10
**Port:** 80 (HTTP)
**Purpose:** Internal web service to simulate hosted applications and test internal HTTPS access

---

### Installtion Steps 
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
