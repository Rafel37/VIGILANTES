# 🦅 Classroom & IP Camera Monitoring Suite

<p align="center">

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Windows-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

</p>

An automated monitoring system developed in **Python** to supervise **classroom computers** and **IP cameras** in educational environments.

The suite detects failures, generates HTML reports, sends email notifications, stores historical records and provides a web dashboard for real-time monitoring.

---

# ✨ Features

- 🖥️ Classroom computer monitoring
- 📷 IP camera monitoring
- 📧 HTML email notifications
- 📊 Historical logging
- 📈 Availability statistics
- 🌐 Web dashboard
- 🛠️ Maintenance mode
- 🚨 Automatic incident detection
- 📅 Daily monitoring reports
- ⚡ Fast and lightweight

---

# 🏗 Architecture

```text
                    +--------------------+
                    |    Maintenance     |
                    +---------+----------+
                              |
                              v
+-----------+       +-------------------+
|   GALLO   |-----> | Classroom Devices |
+-----------+       +-------------------+

+-----------+       +-------------------+
|   LINCE   |-----> |    IP Cameras     |
+-----------+       +-------------------+

        |
        v

+-------------------------------+
| Historical Log (CSV Database) |
+-------------------------------+

        |
        v

+-------------------------------+
| HTML Reports + Email Alerts   |
+-------------------------------+

        |
        v

+-------------------------------+
|     Web Dashboard (Flask)     |
+-------------------------------+
```

---

# 📂 Project Structure

```text
.
├── GALLO_VIRTUAL_EQUIPOS.py
├── LINCE_VIRTUAL_CAMARAS.py
├── SERENO_COBRA_VIRTUAL.py
├── SERENO_LINCE_NOCHE.py
├── VISOR_WEB_PRO.py
├── registros.csv
├── mantenimiento_topo.png
├── requirements.txt
└── README.md
```

---

# 🤖 Monitoring Agents

## 🐓 GALLO

Morning monitoring agent.

Checks classroom computers using ICMP (Ping).

### Responsibilities

- Detect offline computers
- Generate reports
- Send email alerts
- Record incidents

---

## 🐆 LINCE

Camera monitoring agent.

Checks camera availability using ICMP (Ping).

### Responsibilities

- Detect unavailable cameras
- Send HTML reports
- Register incidents
- Generate availability statistics


---

## 🌙 SERENO

Night monitoring agent.

SERENO verifies that all classroom computers have been properly shut down after working hours by performing ICMP (Ping) checks. Since the devices are expected to be powered off, they should **not respond** to the ping requests.

### Responsibilities

- Verify that classroom computers are powered off at night.
- Detect computers that unexpectedly remain online.
- Generate incident reports for devices that respond to Ping.
- Record all detected anomalies.
- Notify administrators when shutdown policies are not followed.

---

## 🐍 COBRA

Automatic shutdown agent.

COBRA acts on the computers detected by SERENO that remain powered on after working hours. It remotely issues shutdown commands to enforce the scheduled power-off policy.

### Responsibilities

- Receive the list of computers still online.
- Send remote shutdown commands.
- Record shutdown operations.
- Help reduce unnecessary energy consumption.
- Ensure compliance with the institution's shutdown policy.

---

## 🛠️ MANTENIMIENTO

Maintenance management module.

Devices under maintenance:

- are excluded from monitoring
- never generate alerts
- receive an independent maintenance report

Example:

```python
MANTENIMIENTO_EQUIPOS = {
    "192.168.0.1": "Classroom 02"
}
```

---

# 📧 Email Reports

The system automatically sends professional HTML reports containing:

- Device status
- IP address
- Availability
- Timestamp
- Monitoring agent
- Embedded images
- Incident summary

---

# 📊 Historical Logs

Every execution is stored in CSV format.

Each record includes:

- Date
- Time
- Agent
- Device
- Status

This information is later used by the dashboard to generate statistics.

---

# 🌐 Web Dashboard

The dashboard provides:

- Real-time monitoring
- Historical incidents
- Availability percentage
- Device status
- Statistics
- Maintenance information



---

# 📦 Technologies

- Python
- Flask
- Tkinter
- Requests
- SMTP
- CSV
- HTML
- Ping (ICMP)


---

# 🎯 Future Improvements

- SQLite database
- Telegram notifications
- Microsoft Teams integration
- Grafana dashboards
- Docker support
- REST API
- Automatic scheduling
- Multi-site monitoring

---

# 📄 License

This project is distributed under the MIT License.

---

# 👨‍💻 Author

**Rafael Pérez Caballero**

Universidad Eclesiástica San Dámaso

Developed to automate the supervision of classroom computers and IP cameras in educational environments.

⭐ If you find this project useful, consider giving it a star on GitHub!
