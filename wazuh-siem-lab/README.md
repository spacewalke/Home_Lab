# 🛡️ Wazuh SIEM Lab — Centralized Logging & Alerting

## 🎯 Goal
Set up a centralized SIEM using Wazuh, onboard multiple hosts as agents, and validate detection rules by simulating typical attack behaviors such as SSH brute-force attempts and port scanning.

---

## ⚙️ Steps

1) **Provision Wazuh VM**  
   - Specs: 4GB RAM, 2 vCPU, 40GB disk  
   - Install Wazuh (Manager + Dashboard) using the **official documentation path**:
   ```bash
   curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
   sudo bash wazuh-install.sh --install-all
   ```
   > I first tried the quick `-a` all‑in‑one flag and ran into GPG key and dashboard startup issues. Following the documented flow fixed it.

2) **Onboard Hosts (Agents)**  
   - From the Wazuh dashboard, I navigated to Agents → Add Agent, selected the OS, and copied the registration command. 
   - Agents were successfully installed on:
     - `docker-host`
     - `pihole`
   - If an agent didn't appear immediately in the dashboard, restarting the agent service and waiting a few minutes helped resolve the issue

3) **Trigger Test Events**
   - SSH brute force (simulate failed logins):
   ```bash
   ssh admin@<vm>
   # Enter wrong password 5–10 times
   ```
   - Port scan (Kali or same VM):
   ```bash
   sudo nmap -sS <target-ip>
   ```

---

## 📊 Results

- **2 active agents** sending logs to Wazuh.
- **Alerts detected** across multiple categories:
  - SSH brute force & failed logins (rules `5710`, `5712`, `5760`)
  - Syslog password misses (`2502`)
  - AppArmor denials (`52004`)
  - File Integrity Monitoring checksum changes (`550`)

**Overview Dashboard**  
![Wazuh Overview Dashboard](images/brave_screenshot-2.png)

**Threat Hunting View**  
![Wazuh Threat Hunting Dashboard](images/brave_screenshot.png)

**Alerts Summary (SSH brute force)**  
![Wazuh Alerts Summary 1](images/brave_screenshot-1.png)

**Alerts Summary (full list)**  
![Wazuh Alerts Summary 2](images/brave_screenshot-3.png)

---


## ⚠️ Challenges Faced
**Quick Installer Failed**
- The fast setup using --a led to GPG key and dashboard startup issues. Switching to the full documented method resolved this.
**Dashboard Didn’t Load Initially**
- Required restarting wazuh-dashboard and elasticsearch services. Checking logs was key in identifying the cause.
**Agent Connection Delays**
- Agents occasionally took several minutes to register. Restarting the agent service usually resolved it.



