# 🦅 Classroom & IP Camera Monitoring Suite (VISOR_WEB_PRO)

<p align="center">

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-2.x-000000?style=for-the-badge&logo=flask&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Windows-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

</p>

An automated monitoring and security suite developed in **Python** and **Flask** to supervise classroom hardware architecture (Windows OPS computers & Android Touch Interactive Panels) as well as AVer IP cameras in educational environments.

The suite handles proactive health checking, remote shutdown execution, dynamic time-window metrics, HTML email reporting, and a real-time web dashboard for IT security operations.

---

# ✨ Features

- 🖥️ **Dual Hardware Monitoring:** Simultaneous status checking for Windows OPS modules and Android Touch Panels per classroom.
- 📷 **AVer IP Camera Tracking:** Dedicated network ping and status verification for IP-connected cameras.
- 🌙 **Automated Energy Saving:** Nighttime compliance enforcement and automated WMI forced power-off (`Win32Shutdown 12`).
- ⚡ **High-Latency Adaptability:** Optimized ICMP parameters (`-n 2 -w 3000`) absorbing boot delays and network standby latency on Android hardware.
- 📧 **Automated HTML Email Reporting:** Embedded status cards and dynamic alerts dispatched after morning and night inspection rounds.
- 🌐 **Interactive Web Dashboard:** Interactive podium of top failing hardware per agent, dynamic success rate gauge, and period toggles (7 days vs. 30 days).
- 🛠️ **Maintenance Mode Management:** Automated exclusion of hardware currently under repair from alerts and calculations.
- 🛡️ **Robust Data Parsing:** Built-in safeguards preventing `TypeError` / `NoneType` rendering errors during CSV parsing.

---

# 🏗 Architecture

```text
                    +--------------------+
                    |  Maintenance Mode  |
                    +---------+----------+
                              |
                              v
+-----------+        +-----------------------------------------+
|   GALLO   |------> | Classroom Devices (OPS Windows &        |
| (Morning) |        |                    Android Touch Panels)|
+-----------+        +-----------------------------------------+

+-----------+        +-----------------------------------------+
|   LINCE   |------> | IP Cameras (AVer Network Hardware)      |
| (Tester)  |        +-----------------------------------------+
+-----------+
      |
      v
+-----------+        +-----------------------------------------+
|  SERENO   |------> | Nightly Shutdown Inspection             |
+-----+-----+        +-----------------------------------------+
      |                           | (Devices still ON)
      |                           v
      |              +-----------------------------------------+
      |              | COBRA (Remote WMI Force Shutdown 12)    |
      |              +-----------------------------------------+
      |                           |
      +---------------------------+
      |
      v
+--------------------------------------------------------------+
| Historical Database (historial_seguridad.csv)                |
+--------------------------------------------------------------+
      |
      +-----------------------------------------+
      |                                         |
      v                                         v
+-------------------------------+ +----------------------------+
| HTML Reports + Email Alerts   | | Web Dashboard (Flask App)  |
| (SMTP with Embedded Media)    | | (7/30-Day Dynamic Filter)  |
+-------------------------------+ +----------------------------+
```

---

# 📂 Project Structure

```text
.
├── GALLO_VIRTUAL_EQUIPOS.py   # Morning startup scan (OPS + Android)
├── LINCE_VIRTUAL_CAMARAS.py    # IP camera connectivity supervisor
├── SERENO_COBRA_FINAL.py      # Nightly verification & automated WMI shutdown
├── VISOR_WEB_PRO.py           # Flask Web Dashboard & detailed report engine
├── historial_seguridad.csv    # Central logging database
├── goodboy_gallo.png          # Status artwork (Gallo OK)
├── badboy_gallo.png           # Status artwork (Gallo Warning)
├── goodboy_sereno.png         # Status artwork (Sereno OK)
├── badboy_sereno.png          # Status artwork (Sereno Warning)
├── cobra.png                  # Execution branding artwork
├── mantenimiento_topo.png     # Maintenance notification banner
└── README.md
```

---

# 🤖 Monitoring Agents & Roles

## 🐓 GALLO (Morning Inspector)
Morning monitoring agent operating at startup.
- **Responsibilities:**
  - Scans both Windows OPS modules and Android Touch Panels across all classrooms.
  - Absorbs initial device boot latencies via high-tolerance pinging.
  - Sends morning availability emails and writes health events to `historial_seguridad.csv`.

## 🐆 LINCE (Camera Supervisor)
Network camera inspection agent.
- **Responsibilities:**
  - Monitors AVer IP camera connectivity across the campus network.
  - Verifies non-invasive device visibility without requiring host PC interaction.
  - Logs camera degradation or total disconnection incidents.

## 🌙 SERENO (Night Vigilance)
After-hours compliance auditor.
- **Responsibilities:**
  - Audits classroom systems after 22:00 PM to verify power-off compliance.
  - Distinguishes between offline (compliant) systems and systems left powered on.
  - Immediately hands over non-compliant OPS hosts to **COBRA**.

## 🐍 COBRA (Shutdown Execution)
Remote remediation agent.
- **Responsibilities:**
  - Receives targets flagged as active by **SERENO**.
  - Issues administrative RPC/WMI forced shutdown calls (`Win32Shutdown 12`) to bypass hung processes.
  - Conducts a follow-up verification scan after 45 seconds to confirm power-down success.

## 🛠️ MANTENIMIENTO (Maintenance Filter)
Hardware isolation subsystem.
- Excludes devices under active repair from routine checks and email alerts.
- Dispatches isolated maintenance summary notifications to administrators.

---

# 📊 Database Schema (`historial_seguridad.csv`)

Events recorded by all agents strictly adhere to the unified CSV schema:

| Column | Description | Example |
| :--- | :--- | :--- |
| `FECHA` | Event Date (`YYYY-MM-DD`) | `2026-11-05` |
| `HORA` | Timestamp (`HH:MM:SS`) | `22:01:15` |
| `AGENTE` | Originating Agent | `GALLO (Mañana)`, `SERENO`, `COBRA` |
| `ESTADO` | Health Status Flag | `OK`, `FALLO` |
| `DETALLES` | Device Identifier & Hardware Tag | `AULA 03 [OPS]`, `AULA 12 [PIZARRA]` |

---

# 🌐 Web Dashboard (`VISOR_WEB_PRO.py`)

The web interface built on Flask provides an operational overview for IT administrators:

- **Interactive Podium:** Top 3 failing rooms categorized per agent (**GALLO**, **LINCE**, **SERENO**).
- **Time Window Toggle:** Live system success percentage computed dynamically over **7 days** or **30 days**.
- **Compact Classroom Grid:** 3-column view matching **Classroom Name**, **OPS (IP + Status Check)**, and **Android Panel (IP + Status Check)**.
- **Detailed Audit Trail:** Filterable log view by date ranges, agent types, and hardware components.

---

# 📦 Requirements & Installation

### Core Dependencies
- Python 3.10+
- Flask

### Installation

```bash
# Clone the repository
git clone https://github.com/your-repo/classroom-monitoring-suite.git
cd classroom-monitoring-suite

# Install dependencies
pip install flask
```

### Running the Web Dashboard

```bash
python VISOR_WEB_PRO.py
```
Access the dashboard at `http://127.0.0.1:5000` or `http://<SERVER_IP>:5000`.

---

# 📄 License

This project is distributed under the **MIT License**.

---

# 👨‍💻 Author

**Rafael Pérez Caballero**  
*Universidad Eclesiástica San Dámaso*  
Developed for automated IT infrastructure maintenance, network camera monitoring, and energy-saving enforcement across university classrooms.
