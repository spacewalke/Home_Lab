# Wazuh TROUBLESHOOTING Guide
**NOTE**
- Most of the commands in this guide require root privileges. Make sure you're either logged in as root or prefix commands with sudo (as shown).

## Install / Service Issues
- **Check services**
- Make sure the core services are running:
  ```bash
  sudo systemctl status wazuh-manager
  sudo systemctl status wazuh-indexer
  sudo systemctl status wazuh-dashboard
  ```
- **View Service Logs**
- If something's notworking, logs are your first stop:
  ```bash
  sudo journalctl -u wazuh-manager -e
  sudo journalctl -u wazuh-indexer -e
  sudo journalctl -u wazuh-dashboard -e
  ```
- **Fixing GPG or Repo key Errors**
  Seeing package signature or key issues during updates or installs? Re-add the Wazuh GPG key and refresh your repo cache:
  ```bash
  curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import
  sudo chmod 644 /usr/share/keyrings/wazuh.gpg || true
  sudo apt update
  ```

## Dashboard Not Loading
- Check Indexer Cluster Health
- A misfiring dashboard often points to indexer issues. Run this to check the cluster:
  ```bash
  curl -k -u admin:admin https://localhost:9200/_cluster/health || true
  ```
- Restart services (in order):
  ```bash
  sudo systemctl restart wazuh-indexer
  sudo systemctl restart wazuh-manager
  sudo systemctl restart wazuh-dashboard
  ```

## Agent Not Showing / No Heartbeat
- Check Agent Connectivity
- Run a quick agent list and ensure firewall rules aren’t blocking communication:
  ```bash
  /var/ossec/bin/agent-control -lc | head
  sudo ufw allow 1514/udp
  sudo ufw allow 1515/tcp
  ```
- Restart agent:
- If an agent isn’t responding, a restart might do the trick:
  ```bash
  sudo systemctl restart wazuh-agent
  sudo systemctl status wazuh-agent
  ```

## Validating Detections
- **SSH brute force**: look for rules `5710`, `5712`, `5760` in *Threat Hunting*.
- **Port scan**: try `sudo nmap -sS <target>` and filter by `rule.id: 8160 OR rule.id: 8161`.
- **Raw logs** (Discover):
  - Queries like: `sshd AND authentication failure`, `nmap`, `apparmor`, `checksum`.

## References & Resources
- https://documentation.wazuh.com/current/index.html
- https://documentation.wazuh.com/current/user-manual/ruleset/ruleset-xml-syntax/rules.html
- https://documentation.wazuh.com/current/installation-guide/firewall.html
- https://www.elastic.co/guide/en/elasticsearch/reference/current/cluster-health.html
