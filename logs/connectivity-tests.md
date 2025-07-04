# Connectivity Test: SSH Access from Kali to Ubuntu

**Date:** [2025-06-03]  
**Tested By:** Bosco Lasrado

---

## Goal
Verify remote access from Kali Linux to Ubuntu Server via SSH.

---

## Test Steps

1. SSH into Ubuntu from Kali:
   ```
   ssh blues@192.168.1.10
   
2. Ran the following commands to confirm successful login and remote control:
   ```
   hostname              # Returned 'ubuntu-srv'
   ip a                 # Confirmed correct IP and network interface
   echo test > ssh-test.txt
   ls -l ssh-test.txt   # File created remotely

3. Logged out of the SSH session with:
   ```
   exit

## Outcome

   - SSH connection successful from Kali → Ubuntu
   - Verified hostname and network
   - Successfully created a file over SSH
   - No issues encountered

## Notes

SSH access is now enabled and can be used for:
   - Remote system management
   - File transfers (scp, rsync)
   - Scripting and automation (Ansible-ready)
