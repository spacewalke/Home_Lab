# 🖥️ Proxmox VE Home Lab — Virtualization & System Administration  
**Hardware:** ZimaBlade • 1TB SSD • DDR3L RAM  

---

## 📌 Project Overview  
I’ve been building a self-hosted virtualization lab on a **ZimaBlade mini-server** using **Proxmox VE**.  
The aim is to have a compact, efficient platform for running multiple VMs and containers, experimenting with services, and honing my sysadmin and security skills — all within my own network.  

---

## ⚙️ Hardware & Software  
- **ZimaBlade Mini-Server**  
- **1TB SSD** (primary storage)  
- **DDR3L SO-DIMM RAM**  
- **Proxmox VE** (latest stable release)  
- Client device for management (**Windows, Linux, or macOS**)  

---

## 🚀 Step-by-Step Build  

### **1️⃣ Hardware Setup**  
- Installed the **1TB SSD** and **DDR3L RAM** into the ZimaBlade  
- Hooked up power, Ethernet, keyboard, mouse, and monitor  

---

### **2️⃣ Installing Proxmox VE**  
- Downloaded the latest **Proxmox VE ISO** from the [official site](https://www.proxmox.com/en/downloads)  
- Flashed the ISO to a USB stick (**Rufus** on Windows / **Balena Etcher** on Mac/Linux)  
- Booted from USB and installed Proxmox VE to the SSD  
- Set **root password**, hostname, timezone, and network configuration  

---

### **3️⃣ Web Interface Access**  
- Opened `https://<server-ip>:8006` in a browser  
- Logged in with **root** credentials set during installation  

---

### **4️⃣ Creating Virtual Machines & Containers**  
- Uploaded OS ISOs (**Ubuntu Server**, **Debian**, **Kali Linux**) to Proxmox storage  
- Created **VMs** with dedicated CPU, RAM, and disk allocations  
- Spun up **LXC containers** for lightweight, service-based workloads  

---

### **5️⃣ Deploying Services**  
- **Docker + Portainer** → Simplified app deployment & management  
- **Pi-hole** → Network-wide ad blocking  
- **Nextcloud / Samba** → File server for personal and shared storage  

---

### **6️⃣ Backup & Snapshot Management**  
- Took **snapshots** before making major changes  
- Scheduled **automated backups** to both local storage and external drives  

---

### **7️⃣ Security Hardening**  
- Enabled **2FA** for Proxmox login  
- Configured **firewall rules** to limit access  
- Set up **SSH key authentication** for secure remote management  

---

## 💡 Future Lab Experiments  
- SOC environment with **Security Onion**  
- Honeypots (**Cowrie**, **Dionaea**) for hands-on threat analysis  
- VLAN & network segmentation testing  
- **ELK stack** for log collection, aggregation, and monitoring  
