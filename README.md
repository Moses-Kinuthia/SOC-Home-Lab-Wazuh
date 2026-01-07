# 🛡️ Enterprise-Grade SOC Monitoring Lab (Wazuh SIEM)

## 🏗️ Project Overview
This repository documents the deployment of a scalable **Security Operations Center (SOC)** lab environment based on the **Wazuh EDR/XDR ecosystem**. The infrastructure is designed to provide full-stack visibility into system events, file integrity, and security posture across a hybrid network environment.

### 🌐 Infrastructure Architecture
* **Manager Node:** Wazuh Server (Ubuntu 22.04 LTS) | Hosted on VirtualBox (Bridged Adapter)
* **Endpoints (Agents):** * **Windows 11 Enterprise (Host):** Real-time monitoring of host-level telemetry and process execution.
  * **Linux (VM):** (*Deployment Pending*) Web Server/Database monitoring.
* **Network Context:** Utilizing a Bridged Networking topology to allow for real-world lateral movement detection and network-level telemetry.

---

## 🛠️ Security Capabilities Implemented
The lab is currently configured to perform the following "Enterprise-Level" functions:

* **Log Data Analysis:** Centralized collection and analysis of Windows Event Logs (Sysmon) and Linux Syslog.
* **Security Configuration Assessment (SCA):** Monitoring for misconfigurations against CIS Benchmarks.
* **Active Response:** (Configuring) Automated intervention based on specific alert triggers.
* **Threat Intel Integration:** Mapping alerts directly to the **MITRE ATT&CK®** framework.

---

## 🧪 Current Focus & Research
I am currently simulating enterprise-level threats to validate detection logic:
1. **Endpoint Monitoring:** Analyzing PowerShell execution and unusual process parenting on the Windows Host.
2. **Network Visibility:** Monitoring cross-device communication via the Bridged network interface.
3. **FIM (File Integrity Monitoring):** Tracking unauthorized changes to sensitive system directories.

---

## 📂 Project Roadmap
- [x] Deployment of Wazuh Manager & Indexer.
- [x] Enrollment of Windows Agent with custom telemetry.
- [ ] Enrollment of Linux Agent for Web Log (Apache/Nginx) monitoring.
- [ ] Integration of **Sysmon** for deep-visibility into Windows kernel events.
- [ ] Simulation of a **Brute-Force Attack** & automated remediation.
- [ ] Implementation of Vulnerability Scanning & Patch Management reporting.

---

## 📊 Dashboard Preview
*(Upload a high-quality screenshot of your Wazuh 'Security events' dashboard to /assets/ and link it here)*
![Wazuh Dashboard](./assets/dashboard_overview.png)

---

## 📜 Disclaimer
This project is for defensive research and educational purposes. All monitoring is performed on owned hardware with explicit consent for data collection.
