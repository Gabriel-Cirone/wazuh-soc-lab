# Wazuh SOC/SIEM Laboratory

> Hands-on Security Operations Center laboratory focused on SIEM,
> endpoint monitoring, log analysis, threat detection and security
> investigation.

![Wazuh](https://img.shields.io/badge/Wazuh-SIEM-blue)
![Windows](https://img.shields.io/badge/Windows-10-blue)
![Linux](https://img.shields.io/badge/Linux-Kali-blue)
![Ubuntu](https://img.shields.io/badge/Ubuntu-Server-orange)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE-ATT%26CK-red)

---

## 📌 Overview

This project documents a hands-on SOC/SIEM laboratory built with
Wazuh.

The environment consists of a Wazuh Manager running on Ubuntu Server,
with Windows 10 and Kali Linux endpoints monitored through Wazuh
Agents.

The objective was to practice the complete security monitoring
workflow:

**Event Generation → Collection → Detection → Analysis → Investigation**

---

## 🎯 Objectives

- Deploy a Wazuh Manager
- Configure Windows and Linux agents
- Collect endpoint telemetry
- Analyze Windows events through Sysmon
- Collect Linux audit events through Auditd
- Monitor file integrity
- Identify vulnerabilities
- Analyze security alerts
- Map detections to MITRE ATT&CK
- Generate and investigate network activity
- Build SIEM dashboards

---

## 🏗️ Architecture

See:

[`architecture/architecture.md`](architecture/architecture.md)

---

## 🖥️ Environment

| Component | Role |
|---|---|
| Ubuntu Server | Wazuh Manager |
| Windows 10 | Monitored Endpoint |
| Kali Linux | Security Testing Endpoint |
| Wazuh Agent | Endpoint Telemetry |
| Sysmon | Windows Telemetry |
| Auditd | Linux Auditing |
| Nmap | Network Security Testing |
| VirtualBox | Virtualization |

---

## 🔎 Security Monitoring

The laboratory covers:

- SIEM
- Endpoint Monitoring
- Log Collection
- Event Analysis
- File Integrity Monitoring
- Vulnerability Detection
- Threat Hunting
- MITRE ATT&CK
- Network Activity Detection

---

## 🧪 Tests

| Test | Status |
|---|---|
| Wazuh Manager | ✅ |
| Windows Agent | ✅ |
| Kali Agent | ✅ |
| Sysmon | ✅ |
| Auditd | ✅ |
| File Integrity Monitoring | ✅ |
| Vulnerability Detection | ✅ |
| MITRE ATT&CK | ✅ |
| Nmap Activity | ✅ |
| SIEM Dashboard | ✅ |

---

## 📊 Evidence

### Wazuh Endpoints

![Wazuh Endpoints](screenshots/01-endpoints.png)

### Wazuh Overview

![Wazuh Overview](screenshots/02-wazuh-overview.png)

### SIEM Dashboard

![SIEM Dashboard](screenshots/03-siem-dashboard.png)

### Vulnerability Detection

![Vulnerability Detection](screenshots/04-vulnerability-detection.png)

### Kali Linux Agent

![Kali Agent](screenshots/05-kali-agent.png)

### Nmap Detection

![Nmap Detection](screenshots/06-nmap-detection.png)

---

## 📚 Documentation

- [Installation](documentation/installation.md)
- [Agent Configuration](documentation/agent-configuration.md)
- [Sysmon](documentation/sysmon.md)
- [Auditd](documentation/auditd.md)
- [File Integrity Monitoring](documentation/fim.md)
- [Vulnerability Detection](documentation/vulnerability-detection.md)
- [Detection & Investigation](documentation/detection-and-investigation.md)

---

## 🧪 Testing Documentation

- [Nmap Test](tests/nmap-test.md)
- [Sysmon Test](tests/sysmon-test.md)
- [Auditd Test](tests/auditd-test.md)
- [FIM Test](tests/fim-test.md)

---

## 📈 Results

See:

[`results/findings.md`](results/findings.md)

---

## 🔐 Security & Privacy

All screenshots published in this repository were sanitized.

The following information was removed or masked:

- IP addresses
- Hostnames
- Hardware information
- Serial numbers
- Machine identifiers
- Other environment-specific information

No credentials, API keys or private keys are included in this repository.

---

## 🧠 Skills Practiced

- Security Operations
- SIEM
- Blue Team
- Endpoint Security
- Log Analysis
- Threat Detection
- Vulnerability Management
- File Integrity Monitoring
- Linux Security
- Windows Security
- MITRE ATT&CK
- Network Security

---

## 🛠️ Technologies

Wazuh · Ubuntu Server · Windows 10 · Kali Linux · Sysmon · Auditd ·
Nmap · MITRE ATT&CK · VirtualBox

---

## 📌 Conclusion

This laboratory provided practical experience with the complete
security monitoring lifecycle, from event generation on endpoints to
centralized collection, detection, visualization and investigation.

The project is part of my ongoing Cybersecurity studies, with a focus
on SOC, Blue Team and Security Operations.
