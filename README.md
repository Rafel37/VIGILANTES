# 🦅 Classroom & IP Camera Monitoring Suite

<p align="center">

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Windows-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

</p>

An automated monitoring system developed in **Python** to supervise **classroom computers (OPS)**, **interactive touch displays (Android)**, and **IP cameras** in educational environments.

The suite detects failures, generates HTML reports, sends email notifications, stores historical records in a CSV database, and provides a real-time web dashboard for system health monitoring.

---

# ✨ Features

- 🖥️ **Dual Classroom Monitoring**: Independent tracking for both OPS (Windows) and Smartboard (Android) devices per classroom.
- 📷 **IP Camera Monitoring**: Connectivity surveillance for security network cameras.
- 📧 **HTML Email Notifications**: Embedded status alerts with custom badge graphics (`GoodBoy` / `BadBoy` / `Cobra` / `Topo`).
- 📊 **Historical CSV Logging**: Automated event registration for uptime and incident tracking.
- 📈 **Dynamic Health Metrics**: 7-day and 30-day statistical availability filters.
- 🌐 **Refactored Web Dashboard**: High-efficiency 3-column UI (`Aula`, `OPS Status`, `Android Status`).
- 🛠️ **Maintenance Mode**: Exclude specific classrooms or devices from automated checking.
- 🚨 **Automatic Remediation**: Forced remote shutdown (`Win32Shutdown 12`) for non-compliant active OPS host computers.
- ⚡ **High Latency Tolerance**: Customized ICMP parameters to eliminate false negatives caused by Android standby responsiveness.

---

# 🏗 Architecture

```text
                    +--------------------+
                    |  Maintenance Mode  |
                    +---------+----------+
                              |
                              v
+-----------+       +------------------------------------+
|   GALLO   |-----> | Classroom Dual Devices             |
+-----------+       | (OPS Windows IP + Android Display) |
                    +------------------------------------+

+-----------+       +------------------------------------+
|   LINCE   |-----> | IP Cameras Network                 |
+-----------+       +------------------------------------+

        |
        v

+--------------------------------------------------------+
| Historical Database (historial_seguridad.csv)          |
+--------------------------------------------------------+

        |
        v

+--------------------------------------------------------+
| HTML Email Reports + Inline CID Graphics               |
+--------------------------------------------------------+

        |
        v

+--------------------------------------------------------+
| Web Dashboard (Flask - 7/30 Day Temporal Filters)     |
+--------------------------------------------------------+
