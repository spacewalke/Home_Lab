# Home_Lab

🖥️ Proxmox VE Home Lab — Virtualization & System Administration
Hardware: ZimaBlade | 1TB SSD | DDR3L RAM

📌 Overview
This project documents my process of building a self-hosted virtualization lab using Proxmox VE on a ZimaBlade server. The goal was to create an environment for running multiple virtual machines (VMs) and containers, hosting services, and practicing system administration and security.

⚙️ Hardware & Software Used
ZimaBlade mini-server

1TB SSD

DDR3L SO-DIMM RAM

Proxmox VE (latest stable release)

Client machine for management (Windows/Linux/Mac)

🚀 Step-by-Step Implementation
1️⃣ Hardware Preparation
Installed 1TB SSD and DDR3L RAM into ZimaBlade.

Connected power, Ethernet, keyboard, mouse, and monitor.

2️⃣ Installing Proxmox VE
Downloaded Proxmox VE ISO from official site.

Flashed the ISO to a USB drive using Rufus.

Booted ZimaBlade from USB and installed Proxmox VE on the SSD.

Set root password, hostname, timezone, and network settings.

3️⃣ Accessing the Web Interface
Logged into https://<server-ip>:8006 from a browser.

Credentials:
User: root
Password: <set during install>
4️⃣ Creating VMs & Containers
Uploaded OS ISOs (Ubuntu Server, Debian, Kali Linux) to Proxmox storage.

Created VMs with allocated CPU, RAM, and disk space.

Created LXC containers for lightweight services.

5️⃣ Deploying Services
Docker + Portainer → App deployment & management.

Pi-hole → Network-wide ad blocker.

File Server (Nextcloud/Samba) → Shared storage.

6️⃣ Backup & Snapshot Management
Created snapshots before major changes.

Configured scheduled backups to local storage and external drives.

7️⃣ Security Hardening
Enabled 2FA for Proxmox login.

Configured firewall rules to limit access.

Set up SSH key authentication.

💡 Lab Ideas
SOC environment with Security Onion.

Honeypots (Cowrie, Dionaea) for threat analysis.

VLAN & network segmentation experiments.

ELK stack for log aggregation and monitoring.

📂 Project Status
In Progress — Actively deploying new services and experimenting with security setups.
