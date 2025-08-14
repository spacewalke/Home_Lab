# Pi-hole DNS Lab — Daily Query Export & Quick Analysis

This repo documents a lightweight DNS monitoring setup using **Pi-hole**. It walks through how to extract **yesterday’s DNS query logs** from the Pi-hole FTL database, transfer the data to your local machine, and perform a basic breakdown of activity.

<img src="images/pihole-yesterday_screenshot.png" alt="Pi-hole Query Log screenshot" width="100%">

---

## 🧪 What’s Inside

This lab demonstrates:

- Real-world DNS traffic visibility using Pi-hole logs.
- A repeatable export pipeline: **FTL (SQLite) → CSV**.
- Lightweight query analysis to identify:
  - Noisy domains
  - DNS patterns
  - Suspicious lookups
- Quick reference for **Pi-hole status codes** (e.g., allowed, blocked, cached).

> 📌 *Note:* Status codes are internal Pi-hole identifiers. Refer to [Pi-hole documentation](https://docs.pi-hole.net/database/ftl/) for details on what each status value means in your version.

---

yaml
Copy
Edit

---

## 📤 Exporting Yesterday’s Queries from Pi-hole

Run the following **on your Pi-hole device** to export the previous day’s queries:

```bash
sudo apt update && sudo apt -y install sqlite3

start=$(date -d 'yesterday 00:00:00' +%s)
end=$(date -d 'today 00:00:00' +%s)

sudo sqlite3 -header -csv /etc/pihole/pihole-FTL.db "
SELECT
  datetime(timestamp,'unixepoch','localtime') AS time,
  client,
  domain,
  type,
  status
FROM queries
WHERE timestamp >= $start AND timestamp < $end
ORDER BY timestamp;
" > ~/pihole-yesterday.csv
Then copy the CSV file to your local machine:

bash
Copy
Edit
scp <user>@<pihole-ip>:~/pihole-yesterday.csv ./pihole-yesterday.csv
💡 Tip: On Windows, you can use WinSCP or a WSL terminal with scp.

📊 Quick Analysis Snapshot
Total queries (yesterday): 5225

🔢 Query Count by Status Code
Status Code	Count
1	278
2	1827
3	1493
5	25
9	94
12	1
14	114
17	1393

🌐 Top 10 Queried Domains
Domain	Count
privacy.aurasvc.io	814
d2y36twrtb17ty.cloudfront.net	314
status.zybooks.com	307
wgu.hosted.panopto.com	248
api.aurasvc.io	206
wpad.mynetworksettings.com	170
heapanalytics.com	106
kv801.prod.do.dsp.mp.microsoft.com	101
cdn-checkout.joinhoney.com	96
go-updater.brave.com	87

🔍 Investigation Tips:

Look for high-frequency domains (telemetry, trackers, CDNs).

Investigate random-looking subdomains or unusual TLDs.

Check which client IPs generate the most requests.

✅ Use Cases
This workflow is useful for:

Threat hunting on home or lab networks

Tracking telemetry / ad domains

Troubleshooting noisy devices

Teaching DNS forensics and fundamentals

🛡️ Disclaimer
This tool is intended for educational and monitoring use on networks you own or are authorized to analyze. Ensure compliance with local laws and privacy regulations.



