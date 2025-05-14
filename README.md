# Cyber-Security-LAB
installing a Linux server on VirtualBox and setting up SSH. This guide assumes you're installing Ubuntu Server (you can adapt it for Debian, CentOS, etc.).

---

# 🐧 Linux Server Installation on VirtualBox + SSH Setup

This guide walks you through setting up a Linux server on VirtualBox and configuring SSH for remote access.

---

## 🧰 Prerequisites

* [VirtualBox](https://www.virtualbox.org/) installed
* [Ubuntu Server ISO](https://ubuntu.com/download/server) downloaded
* Optional: [VirtualBox Extension Pack](https://www.virtualbox.org/wiki/Downloads)

---

## 🚀 Step-by-Step Guide

### 1. **Create a New Virtual Machine**

1. Open VirtualBox → Click **New**
2. Name: `UbuntuServer`
   Type: `Linux`
   Version: `Ubuntu (64-bit)`
3. Memory Size: **2048 MB** (Recommended)
4. Hard Disk:

   * Create a virtual hard disk now → VDI → Dynamically allocated
   * Size: **20 GB** (Minimum)

---

### 2. **Mount ISO and Install Ubuntu Server**

1. Select the VM → Click **Settings** → **Storage**
2. Under **Controller: IDE**, click the empty disk icon → Choose the downloaded **Ubuntu Server ISO**
3. Start the VM → Follow installation prompts:

   * Language and Region
   * Network Configuration
   * Set hostname and user credentials
   * Use entire disk for storage
   * Enable **OpenSSH Server** during setup (important!)
   * Wait for installation to finish
4. Reboot when done, and remove ISO when prompted

---

### 3. **(Optional) Install SSH Manually**

If you didn't enable SSH during installation, do the following:

1. Log into the virtual machine
2. Update and install SSH:

   ```bash
   sudo apt update
   sudo apt install openssh-server
   ```
3. Check SSH status:

   ```bash
   sudo systemctl status ssh
   ```

---

### 4. **Configure Port Forwarding (to Access via SSH)**

1. VM Settings → **Network** → Adapter 1 → Attached to: **NAT**
2. Click **Advanced** → **Port Forwarding**

   * Name: `SSH`
   * Protocol: `TCP`
   * Host Port: `2222`
   * Guest Port: `22`

---

### 5. **Access Your Server via SSH**

On your host machine (Linux/macOS/Git Bash):

```bash
ssh username@localhost -p 2222
```

> Replace `username` with the one you set during installation.

---

## 🧪 Troubleshooting

* **SSH Connection Refused**: Ensure SSH is installed and running (`sudo systemctl status ssh`)
* **Slow Network**: Try switching to **Bridged Adapter** in network settings
* **Permission Denied**: Check if you're using the correct username and port

---

## 📌 Notes

* Default SSH port is `22`; we used `2222` on the host to avoid conflicts.
* Keep your server updated:

  ```bash
  sudo apt update && sudo apt upgrade
  ```

---

## ✅ You're All Set!

You now have a running Linux server in VirtualBox with SSH access. Happy hacking!
