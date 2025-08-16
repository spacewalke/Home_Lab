# TROUBLESHOOTING

## Install / Service Issues
- **Check services**
  ```bash
  sudo systemctl status wazuh-manager
  sudo systemctl status wazuh-indexer
  sudo systemctl status wazuh-dashboard
  ```
- **Logs**
  ```bash
  sudo journalctl -u wazuh-manager -e
  sudo journalctl -u wazuh-indexer -e
  sudo journalctl -u wazuh-dashboard -e
  ```
- **GPG / Repo key**
  If package key errors occur, (re)add the Wazuh key and update:
  ```bash
  curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH |         sudo gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import
  sudo chmod 644 /usr/share/keyrings/wazuh.gpg || true
  sudo apt update
  ```

## Dashboard Not Loading
- Ensure indexer cluster is healthy:
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
- Verify connectivity:
  ```bash
  /var/ossec/bin/agent-control -lc | head
  sudo ufw allow 1514/udp
  sudo ufw allow 1515/tcp
  ```
- Restart agent:
  ```bash
  sudo systemctl restart wazuh-agent
  sudo systemctl status wazuh-agent
  ```

## Validating Detections
- **SSH brute force**: look for rules `5710`, `5712`, `5760` in *Threat Hunting*.
- **Port scan**: try `sudo nmap -sS <target>` and filter by `rule.id: 8160 OR rule.id: 8161`.
- **Raw logs** (Discover):
  - Queries like: `sshd AND authentication failure`, `nmap`, `apparmor`, `checksum`.
