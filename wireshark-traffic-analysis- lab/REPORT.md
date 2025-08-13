# Wireshark + Traffic Analysis — Report (1 page)

## Environment
- Capture host: Ubuntu Server VM (no GUI) — tshark for packet capture
-Analysis host: Local machine with Wireshark GUI
-Interface: ens18
-Capture duration: 120 seconds

## Methods
1. Installed tshark on Ubuntu Server and granted non-root capture permissions.
2. Ran: `tshark -i <iface> -a duration:120 -w ~/capture.pcapng`.
3. Generated traffic during capture:
   - `ping -c 5 8.8.8.8`
   - `curl example.com`
   - `curl https://wikipedia.org`
   - (optional) `dig example.com`
4. Transferred capture to local machine via `scp` and analyzed in Wireshark with filters:
   - DNS: `dns`
   - TCP SYN (3‑way handshake start): `tcp.flags.syn==1 && tcp.flags.ack==0`
   - HTTP: `http`
   - HTTPS/TLS: `tls`

## Findings

### Packet Counts (from Wireshark filter results)
-DNS queries observed: 6
-TCP connections initiated (SYNs): 2
-HTTP sessions: 0 (all observed web requests used HTTPS)
-HTTPS/TLS sessions (Client Hellos): 3

### Evidence
- **DNS**: Queries for  `wikipedia.org`, `youtube.com`, `yahoo.com`.
- **TCP Handshake**: Observed SYN → SYN/ACK → ACK to destination port 443.
- **HTTPS**: TLS 1.3 Client Hello / Server Hello and subsequent encrypted application data.

(See `screenshots/` folder — include a Packet List view and a Packet Details view.)

## Interpretation
### Traffic observed matches typical web browsing and basic diagnostic activity:
- DNS lookups precede outbound TCP connections.  
- TCP 3-way handshakes occur before encrypted sessions.  
- All web traffic used TLS; no HTTP payloads were visible.  
- No signs of scanning, anomalous protocols, or unusual destinations in the short capture window.  
- No anomalous behaviors detected in this short baseline capture window.  

## Appendix
**Core commands used**
```bash
sudo apt update && sudo apt -y install tshark
sudo usermod -aG wireshark $USER && newgrp wireshark
tshark -i <iface> -a duration:120 -w ~/capture.pcapng

# Traffic generation
ping -c 5 8.8.8.8
curl example.com
curl https://wikipedia.org

# Transfer capture for analysis
scp <user>@<vm-ip>:~/capture.pcapng .
```
