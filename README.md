# 🔐 Smart Cybersecurity Router - Behavioral Intelligence Edition

# NETSHIELD AI

An intelligent network monitoring and access control system for modern households, student dorms, and smart homes.  
This Python-based system empowers you to **see, understand, and control** all the devices connected to your local network — in real time.

---

## 🧠 Key Features

### 🔍 Real-Time Device Discovery & Monitoring
- Automatically detects connected devices via ARP, DHCP, and Nmap.
- Captures and analyzes traffic using `tcpdump` + `pyshark`.
- Enriches device metadata with MAC vendor lookups.

### 📊 Behavioral Fingerprinting
- Categorizes traffic into:
  - Streaming | Gaming | Work | Social | Search | Unknown
- Tracks:
  - Active hours
  - Frequently visited domains
  - Behavioral patterns across days
- Saves historical activity logs in machine-readable JSON files.

### 🔐 Access Control (Phase 3)
- MAC-based Firewall Enforcement (via `iptables`)
- DNS Blocking (via `dnsmasq`)
- Per-device restrictions:
  - Blocked websites
  - Time-based usage schedules (e.g. block social apps after 9 PM)

### 🧾 Usage Reports & Logs
- Daily usage summary generator
- JSON-based logs for visualization-ready dashboards
- Optional report scheduler (auto runs at midnight)

---

## ⚙️ Requirements

### System Dependencies
Install these via `apt` (Debian/Ubuntu):

```bash
sudo apt install arp-scan tcpdump tshark nmap dnsmasq iptables netfilter-persistent
```

### Python Libraries

```bash
pip install -r requirements.txt
```

> Or manually:
```bash
pip install pyshark requests
```

---

## 🚀 Getting Started

1. **Run as Root (Important)**

```bash
sudo python3 smart_cybersec_router.py
```

2. Logs and state will be automatically saved to the `log_data/` directory.
3. Access control and fingerprinting are updated dynamically.

---

## 📋 Configuration

- **Interface:** Default is `wlan0`. Update `INTERFACE` if needed.
- **Blocklist:** Auto-syncs from [StevenBlack/hosts](https://github.com/StevenBlack/hosts)
- **Parental Controls:** Define MAC-based restrictions in `PARENTAL_CONTROLS`:

```python
PARENTAL_CONTROLS = {
    "AA:BB:CC:DD:EE:FF": {
        "name": "Kid's Laptop",
        "blocked_sites": ["instagram.com", "tiktok.com"],
        "time_restrictions": {"22:00-06:00": "block_all"}
    }
}
```

---

## 🛡️ Architecture Overview

```plaintext
[ARP / DHCP] --> Device Discovery
   |
   v
[Traffic Capture] --> [pyshark Analysis] --> Categorization + Domain Extraction
   |
   v
[Behavioral Fingerprinting] + [Access Control Enforcement]
   |
   v
[Logs + Enriched Device State] --> Dashboard / Visualization Ready
```

---

## 📈 Future Additions

- 📡 Web Dashboard (FastAPI + React or Flask)
- 🧠 Threat Anomaly Detection
- 🔁 Auto-Learning Device Classification
- 🧩 Integrate with PhantomShield AI or SOAR tools

---

## 📜 License

MIT License — use freely, fork wildly, contribute generously.

---
