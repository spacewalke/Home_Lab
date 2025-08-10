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
