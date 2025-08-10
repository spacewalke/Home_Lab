# 🖥️ Proxmox VE Home Lab — Virtualization & System Administration  
**Hardware:** ZimaBlade | 1TB SSD | DDR3L RAM  

## 📌 Overview  
This project documents my process of building a **self-hosted virtualization lab** using **Proxmox VE** on a ZimaBlade server.  
The goal was to create an environment for running multiple virtual machines (VMs) and containers, hosting services, and practicing system administration and security.  

---

## ⚙️ Hardware & Software Used  
- **ZimaBlade** mini-server  
- **1TB SSD**  
- **DDR3L SO-DIMM RAM**  
- **Proxmox VE** (latest stable release)  
- **Client machine** for management (Windows/Linux/Mac)  

---

## 🚀 Step-by-Step Implementation  

### **1️⃣ Hardware Preparation**  
- Installed **1TB SSD** and **DDR3L RAM** into ZimaBlade  
- Connected **power**, **Ethernet**, keyboard, mouse, and monitor  

---

### **2️⃣ Installing Proxmox VE**  
- Downloaded **Proxmox VE ISO** from [official site](https://www.proxmox.com/en/downloads)  
- Flashed the ISO to a USB drive using **Rufus** (Windows) or **Balena Etcher** (Mac/Linux)  
- Booted ZimaBlade from USB and installed Proxmox VE on the SSD  
- Set **root password**, hostname, timezone, and network settings  

---

### **3️⃣ Accessing the Web Interface**  
- Logged into `https://<server-ip>:8006` from a browser  
- **Credentials:**  


---

### **4️⃣ Creating VMs & Containers**  
- Uploaded OS ISOs (Ubuntu Server, Debian, Kali Linux) to Proxmox storage  
- Created **VMs** with allocated CPU, RAM, and disk space  
- Created **LXC containers** for lightweight services  

---

### **5️⃣ Deploying Services**  
- **Docker + Portainer** → App deployment & management  
- **Pi-hole** → Network-wide ad blocker  
- **File Server (Nextcloud/Samba)** → Shared storage  

---

### **6️⃣ Backup & Snapshot Management**  
- Created **snapshots** before major changes  
- Configured **scheduled backups** to local storage and external drives  

---

### **7️⃣ Security Hardening**  
- Enabled **2FA** for Proxmox login  
- Configured **firewall rules** to limit access  
- Set up **SSH key authentication**  

---

## 💡 Lab Ideas  
- SOC environment with **Security Onion**  
- Honeypots (Cowrie, Dionaea) for threat analysis  
- VLAN & network segmentation experiments  
- ELK stack for log aggregation and monitoring  

---

## 📂 Project Status  
**In Progress** — Actively deploying new services and experimenting with security setups  

---

## 🔗 Resources  
- [Proxmox VE Documentation](https://pve.proxmox.com/wiki/Main_Page)  
- [Docker Documentation](https://docs.docker.com/)  
- [Pi-hole Setup Guide](https://pi-hole.net/)  





🖥️ Proxmox VE Home Lab — Virtualization & System Administration
Hardware: ZimaBlade • 1TB SSD • DDR3L RAM

📌 Project Overview
I’ve been building a self-hosted virtualization lab on a ZimaBlade mini-server using Proxmox VE.
The aim is to have a compact, efficient platform for running multiple VMs and containers, experimenting with services, and honing my sysadmin and security skills—all within my own network.

⚙️ Hardware & Software
ZimaBlade Mini-Server

1TB SSD (primary storage)

DDR3L SO-DIMM RAM

Proxmox VE (latest stable release)

Client device for management (Windows, Linux, or macOS)

🚀 Step-by-Step Build
1️⃣ Hardware Setup
Installed the 1TB SSD and DDR3L RAM into the ZimaBlade

Hooked up power, Ethernet, keyboard, mouse, and monitor

2️⃣ Installing Proxmox VE
Downloaded the latest Proxmox VE ISO from the official site

Flashed the ISO to a USB stick (Rufus on Windows / Balena Etcher on Mac/Linux)

Booted from USB and installed Proxmox VE to the SSD

Set root password, hostname, timezone, and network config

3️⃣ Web Interface Access
Opened https://<server-ip>:8006 in a browser

Logged in with root credentials set during installation

4️⃣ Creating Virtual Machines & Containers
Uploaded OS ISOs (Ubuntu Server, Debian, Kali Linux) to Proxmox storage

Created VMs with dedicated CPU, RAM, and disk allocations

Spun up LXC containers for lightweight, service-based workloads

5️⃣ Deploying Services
Docker + Portainer → Simplified app deployment & management

Pi-hole → Network-wide ad blocking

Nextcloud / Samba → File server for personal and shared storage

6️⃣ Backup & Snapshot Management
Took snapshots before making major changes

Scheduled automated backups to both local storage and external drives

7️⃣ Security Hardening
Enabled 2FA for Proxmox login

Configured firewall rules to limit access

Set up SSH key authentication for secure remote management

💡 Future Lab Experiments
SOC environment with Security Onion

Honeypots (Cowrie, Dionaea) for hands-on threat analysis

VLAN & network segmentation testing

ELK stack for log collection, aggregation, and monitoring

📂 Current Status
In Progress — New services are being deployed, and security experiments are ongoing.
The goal is to make this lab a sandbox for everything from virtualization experiments to incident response practice.
