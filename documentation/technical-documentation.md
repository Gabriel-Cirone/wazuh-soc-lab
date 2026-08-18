# Wazuh SOC/SIEM Laboratory — Technical Documentation

---

# 1. Introduction

This project consists of the implementation of a **Security Information and Event Management (SIEM)** laboratory using **Wazuh**.

The main objective was to build a controlled environment capable of simulating part of the operation of a **Security Operations Center (SOC)**.

The laboratory was built using virtual machines and consisted of:

* **Ubuntu Server 24.04** — Wazuh Server;
* **Windows 10** — monitored Windows endpoint;
* **Kali Linux** — monitored Linux endpoint and controlled security-testing machine.

Throughout the project, we configured centralized security monitoring, endpoint agents, Windows Sysmon, Linux Auditd, File Integrity Monitoring, vulnerability detection, MITRE ATT&CK visibility, and controlled security tests.

The project followed the complete monitoring process:

```text
Endpoint
   ↓
Data Collection
   ↓
Wazuh Agent
   ↓
Wazuh Server
   ↓
Event Processing
   ↓
Wazuh Indexer
   ↓
Wazuh Dashboard
   ↓
Investigation
```

---

# 2. Project Objectives

The main objectives of the laboratory were:

* Install and configure Wazuh;
* Create a centralized SIEM environment;
* Configure Ubuntu Server as the Wazuh server;
* Connect Windows 10 as a monitored endpoint;
* Connect Kali Linux as a monitored endpoint;
* Collect Windows security events;
* Configure Sysmon;
* Collect Linux audit events using Auditd;
* Configure File Integrity Monitoring;
* Monitor endpoint vulnerabilities;
* Investigate security alerts;
* Analyze events using the Wazuh Dashboard;
* Associate security events with MITRE ATT&CK;
* Generate controlled security events;
* Practice SOC investigation;
* Practice troubleshooting of a security monitoring infrastructure.

---

# 3. Laboratory Architecture

The laboratory used an **all-in-one Wazuh deployment**.

In this architecture, the main Wazuh components were installed on the Ubuntu Server:

* Wazuh Server;
* Wazuh Indexer;
* Wazuh Dashboard.

The Windows and Kali Linux systems were configured as endpoints with the Wazuh Agent installed.

The architecture can be represented as:

```text
                  ┌─────────────────────────┐
                  │     Wazuh Dashboard     │
                  │      Web Interface      │
                  └────────────┬────────────┘
                               │
                               ▼
                  ┌─────────────────────────┐
                  │      Wazuh Indexer      │
                  │   Storage and Search    │
                  └────────────┬────────────┘
                               │
                               ▼
                  ┌─────────────────────────┐
                  │      Wazuh Server       │
                  │    Analysis / Manager   │
                  └────────────┬────────────┘
                               │
                 ┌─────────────┴─────────────┐
                 │                           │
                 ▼                           ▼
        ┌─────────────────┐         ┌─────────────────┐
        │    Windows 10   │         │    Kali Linux   │
        │                 │         │                 │
        │  Wazuh Agent    │         │  Wazuh Agent    │
        │  Sysmon         │         │  Auditd         │
        └─────────────────┘         └─────────────────┘
```

The complete data flow is:

```text
Endpoint
   ↓
Wazuh Agent
   ↓
Wazuh Server
   ↓
Wazuh Indexer
   ↓
Wazuh Dashboard
```

---

# 4. Virtualization Environment

The entire laboratory was deployed using virtual machines.

The host system provided approximately:

* **16 CPUs**
* **24 GB RAM**

These resources were distributed between the Ubuntu Server, Windows 10, and Kali Linux virtual machines.

The purpose of using virtualization was to create an isolated environment where different systems could communicate with each other while remaining separate from the host operating system.

This also allowed security tests to be performed without affecting a production environment.

---

# 5. Ubuntu Server Installation

The first system configured was **Ubuntu Server 24.04**.

The Ubuntu Server was used as the central Wazuh infrastructure.

After installing the operating system, the initial configuration included:

* Updating the system;
* Installing required packages;
* Configuring the network;
* Checking the IP address;
* Verifying connectivity;
* Configuring the hostname;
* Testing communication with the other virtual machines.

The network configuration was particularly important because the Wazuh Agents needed to communicate with the central Wazuh Server.

---

# 6. Wazuh Installation

After preparing Ubuntu Server, the Wazuh infrastructure was installed.

The deployment consisted of three main components.

## 6.1 Wazuh Server

The Wazuh Server is responsible for receiving and analyzing security information from the agents.

Its responsibilities include:

* Receiving events;
* Decoding logs;
* Applying detection rules;
* Generating alerts;
* Processing security events;
* Managing agents.

The Wazuh Server is therefore the central processing component of the laboratory.

---

## 6.2 Wazuh Indexer

The Wazuh Indexer is responsible for storing and indexing the data processed by the Wazuh Server.

This allows events to be:

* Stored;
* Indexed;
* Searched;
* Retrieved;
* Investigated later.

Without the Indexer, the Dashboard would not have the centralized data required for investigation.

---

## 6.3 Wazuh Dashboard

The Wazuh Dashboard is the graphical interface used to interact with the platform.

Through the Dashboard, it is possible to view:

* Agents;
* Security alerts;
* Events;
* Severity levels;
* Vulnerabilities;
* File Integrity Monitoring;
* MITRE ATT&CK information;
* Endpoint inventory;
* Security-related data.

The Dashboard became the main interface used during the investigation stages of the laboratory.

---

# 7. Network Communication

Understanding network communication between the Wazuh components was an important part of the implementation.

Some of the main ports used by Wazuh are:

| Port        | Function            |
| ----------- | ------------------- |
| `1514/TCP`  | Agent communication |
| `1515/TCP`  | Agent enrollment    |
| `55000/TCP` | Wazuh API           |
| `9200/TCP`  | Wazuh Indexer API   |
| `443/TCP`   | Wazuh Dashboard     |

The Wazuh Agent needs to communicate with the Wazuh Server in order to send collected security events.

Therefore, connectivity was verified before troubleshooting the agents themselves.

---

# 8. Wazuh Dashboard Configuration

After installing the Wazuh infrastructure, the Dashboard was accessed through a web browser.

The Dashboard provided centralized visibility into the laboratory.

From the Dashboard, we could monitor:

* Connected agents;
* Security alerts;
* Events;
* Event severity;
* File changes;
* Vulnerabilities;
* MITRE ATT&CK information;
* Endpoint information.

The Dashboard was also used later to investigate the events generated during the controlled security tests.

---

# 9. Windows 10 Endpoint Configuration

Windows 10 was configured as the first monitored endpoint.

The **Wazuh Agent** was installed on the Windows machine.

The agent was configured to communicate with the Wazuh Server.

The communication flow became:

```text
Windows 10
     ↓
Wazuh Agent
     ↓
Wazuh Server
```

After installation, the Windows agent was registered with the Wazuh Server.

The Dashboard was then used to verify whether the agent was visible and whether its status was active.

---

# 10. Windows Agent Troubleshooting

During the Windows configuration, the agent initially did not appear correctly in the Wazuh Dashboard.

The troubleshooting process involved checking several points.

## 10.1 Agent Service

The Wazuh Agent service was checked to ensure that it was installed and running.

## 10.2 Agent Configuration

The configuration was checked to ensure that the Wazuh Server address was correct.

## 10.3 Network Connectivity

Connectivity between Windows and Ubuntu Server was verified.

## 10.4 Agent Registration

The enrollment process was checked to ensure that the Windows endpoint was correctly registered.

## 10.5 Administrative Permissions

Some commands required administrative privileges on Windows.

After correcting the configuration and permissions, the Windows Agent successfully communicated with the Wazuh Server.

This troubleshooting process demonstrated an important real-world SOC infrastructure skill: determining whether a monitoring problem originates from the endpoint, network, agent configuration, or central server.

---

# 11. Sysmon Installation on Windows

After configuring the Wazuh Agent, **Microsoft Sysmon** was installed on Windows.

Sysmon provides detailed telemetry about activities occurring within Windows.

It can generate events related to:

* Process creation;
* Network connections;
* File activity;
* Process behavior;
* Other system activities relevant to security analysis.

The purpose of Sysmon in this project was to provide additional telemetry to the Wazuh SIEM.

The data flow became:

```text
Windows Activity
       ↓
     Sysmon
       ↓
Windows Event Log
       ↓
Wazuh Agent
       ↓
Wazuh Server
       ↓
Wazuh Indexer
       ↓
Wazuh Dashboard
```

This provided considerably more visibility into Windows activity.

---

# 12. Sysmon and Wazuh Integration

After installing Sysmon, the Wazuh Agent was configured to collect the corresponding Windows Event Log information.

This allowed Sysmon events to be forwarded to the Wazuh Server.

The objective was not simply to collect raw events.

The goal was to allow Wazuh to:

1. Receive the event;
2. Decode the event;
3. Apply detection rules;
4. Generate an alert when appropriate;
5. Store the event;
6. Make the event available through the Dashboard.

This created a more realistic endpoint monitoring environment.

---

# 13. Sysmon Troubleshooting

During the Sysmon configuration, we encountered an issue where the Sysmon executable was not being recognized correctly.

The installation and execution configuration were verified.

After correcting the issue, Sysmon was successfully running and generating Windows telemetry.

This demonstrated the importance of validating the individual components of a monitoring pipeline.

Before investigating Wazuh itself, it was necessary to confirm that the endpoint was actually generating the expected events.

---

# 14. Kali Linux Configuration

Kali Linux was configured as the second monitored endpoint.

The Kali machine had two purposes:

1. Act as a monitored Linux endpoint;
2. Perform controlled security tests against the laboratory.

The Wazuh Agent was installed and configured on Kali Linux.

The resulting environment was:

```text
Kali Linux
   │
   ├── Wazuh Agent
   ├── Auditd
   └── Nmap
```

This allowed the Wazuh Server to receive telemetry from both Windows and Linux.

---

# 15. Auditd Configuration

**Auditd** was configured on Kali Linux.

Auditd is part of the Linux Audit Framework and provides auditing capabilities for Linux systems.

It records security-related activity that can later be analyzed by security professionals.

The telemetry flow became:

```text
Activity on Kali Linux
        ↓
      Auditd
        ↓
    Audit Logs
        ↓
   Wazuh Agent
        ↓
   Wazuh Server
        ↓
 Wazuh Indexer
        ↓
 Wazuh Dashboard
```

The objective was to ensure that Linux audit events generated by Auditd could be collected by Wazuh and viewed in the Dashboard.

---

# 16. Auditd Validation and Troubleshooting

One of the validation tasks was checking whether Auditd events were correctly reaching the Wazuh Dashboard.

The complete data path was analyzed:

```text
Auditd
   ↓
Audit Logs
   ↓
Wazuh Agent
   ↓
Wazuh Server
   ↓
Wazuh Indexer
   ↓
Wazuh Dashboard
```

This was important because an event not appearing in the Dashboard does not necessarily mean that the SIEM itself is malfunctioning.

The problem could exist at any stage:

```text
Data Source
     ↓
Collection
     ↓
Transport
     ↓
Processing
     ↓
Storage
     ↓
Visualization
```

This troubleshooting methodology is directly applicable to real SIEM environments.

---

# 17. File Integrity Monitoring

The laboratory also explored **File Integrity Monitoring (FIM)**.

FIM allows Wazuh to monitor selected files and detect changes.

The basic process is:

```text
Original File
     ↓
Baseline / Hash
     ↓
File Modification
     ↓
Wazuh Detection
     ↓
Alert
```

FIM can help identify:

* Unauthorized file modifications;
* Configuration changes;
* Changes to critical files;
* Potential indicators of compromise.

File integrity monitoring is particularly useful in defensive security because unauthorized modifications can be an indicator of malicious activity.

---

# 18. Endpoint Inventory

The Wazuh inventory capabilities were also explored.

Inventory provides information about the monitored endpoints.

Examples include:

* Operating system;
* Hardware;
* Installed software;
* Packages;
* System information.

This information is important during security investigations.

When an alert is generated, the analyst needs to understand which asset generated the event and what software and operating system are present on that asset.

---

# 19. Vulnerability Detection

The Wazuh environment was also used to monitor vulnerabilities present on the endpoints.

The general process can be represented as:

```text
Endpoint
   ↓
Installed Software
   ↓
Software Version
   ↓
Known Vulnerability
   ↓
CVE
   ↓
Severity / Risk
```

This capability adds vulnerability visibility to the SIEM environment.

Instead of only monitoring security events, the platform can also provide information about weaknesses in the monitored systems.

---

# 20. MITRE ATT&CK

The Wazuh environment was also used to associate security events with the **MITRE ATT&CK framework**.

MITRE ATT&CK provides a structured knowledge base of adversary tactics and techniques.

The relationship can be represented as:

```text
Security Event
      ↓
Wazuh Rule
      ↓
Detection
      ↓
MITRE ATT&CK
      ↓
Tactic / Technique
```

This allows an analyst to understand the potential behavior represented by an event.

Instead of analyzing an alert only as an isolated log entry, the analyst can consider whether it represents behavior associated with a known adversary technique.

---

# 21. Generation of Controlled Security Events

After the monitoring environment was fully configured, controlled security activities were performed.

One of the main tools used was **Nmap**.

Nmap was executed from Kali Linux to perform controlled network reconnaissance against the laboratory environment.

The objective was not to compromise the systems.

The objective was to generate observable network activity and verify whether the monitoring infrastructure could detect and display the resulting events.

The process was:

```text
Kali Linux
     │
     │ Nmap
     ▼
Laboratory Target
     │
     ▼
Network Activity
     │
     ▼
Wazuh
     │
     ▼
Events / Alerts
     │
     ▼
Dashboard
```

All testing was performed within the controlled laboratory environment.

---

# 22. Event Investigation

After generating the controlled activity, the Wazuh Dashboard was used to locate the corresponding events.

The investigation focused on information such as:

* Timestamp;
* Source endpoint;
* Source IP address;
* Event type;
* Severity;
* Rule ID;
* Event description;
* MITRE ATT&CK information when available.

The investigation workflow followed:

```text
Detection
   ↓
Contextualization
   ↓
Investigation
   ↓
Classification
```

This represents a simplified SOC analyst workflow.

---

# 23. Event Filtering

Filtering was an important part of the investigation process.

A SIEM can receive a large amount of telemetry.

Therefore, analyzing every event individually is not practical.

The Wazuh Dashboard allows events to be filtered using fields such as:

* Agent;
* IP address;
* Rule;
* Alert level;
* Timestamp;
* Event type;
* Specific event fields.

This allowed the events generated during the controlled tests to be isolated and analyzed more efficiently.

---

# 24. Agent Validation

After completing the configuration of both endpoints, the Wazuh Dashboard was used to verify the agent status.

The final environment contained:

```text
Windows 10
Wazuh Agent
Status: Active
```

and:

```text
Kali Linux
Wazuh Agent
Status: Active
```

This confirmed that both endpoints were successfully communicating with the Wazuh Server.

Agent validation was performed before the security tests to ensure that the generated events would actually be collected.

---

# 25. Complete Data Flow

The complete monitoring architecture can be summarized as:

```text
                    WINDOWS 10
                 ┌──────────────┐
                 │    Sysmon    │
                 └──────┬───────┘
                        │
                        ▼
                 Windows Events
                        │
                        ▼
                  Wazuh Agent
                        │
                        ▼
              ┌─────────────────┐
              │  Wazuh Server   │
              │                 │
              │ Decoders        │
              │ Rules           │
              │ Analysis        │
              │ Alerts          │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │ Wazuh Indexer  │
              │                 │
              │ Storage         │
              │ Indexing        │
              │ Search          │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │ Wazuh Dashboard │
              │                 │
              │ Alerts          │
              │ Events          │
              │ FIM             │
              │ Vulnerabilities │
              │ MITRE ATT&CK    │
              └─────────────────┘
                       ▲
                       │
                  Wazuh Agent
                       ▲
                       │
              ┌────────┴────────┐
              │   Kali Linux   │
              │                │
              │    Auditd      │
              │    Nmap        │
              └────────────────┘
```

---

# 26. SOC Workflow

The laboratory was designed to simulate a simplified SOC workflow.

The general process was:

```text
          EVENT
            ↓
        COLLECTION
            ↓
           SIEM
            ↓
        DETECTION
            ↓
      INITIAL TRIAGE
            ↓
       INVESTIGATION
            ↓
      RISK ANALYSIS
            ↓
         RESPONSE
            ↓
       DOCUMENTATION
```

In the laboratory, Wazuh was responsible for the majority of the technical monitoring process:

* Collecting telemetry;
* Processing events;
* Applying detection rules;
* Generating alerts;
* Storing information;
* Providing investigation capabilities.

The analyst's role is to interpret this information and determine whether an event represents legitimate, suspicious, or potentially malicious activity.

---

# 27. Troubleshooting Performed

Troubleshooting was an important part of the project.

The main problems investigated included:

## 27.1 Windows Agent

The Windows Agent initially did not appear correctly in the Wazuh Dashboard.

The issue was investigated through service, configuration, network, enrollment, and permission checks.

---

## 27.2 Sysmon

The Sysmon executable was initially not recognized correctly.

The installation and execution configuration were verified and corrected.

---

## 27.3 Auditd

The Auditd data pipeline was verified from the Linux audit logs through the Wazuh Agent and Server until the Dashboard.

---

## 27.4 Network Connectivity

Connectivity between the endpoints and Wazuh Server was verified to ensure that the agents could communicate correctly.

---

# 28. Security and Privacy Considerations

Before publishing screenshots or configuration files, sensitive information should be reviewed and removed when necessary.

Examples include:

* Public IP addresses;
* Personal usernames;
* Personal hostnames;
* MAC addresses;
* Passwords;
* API keys;
* Authentication tokens;
* Other personally identifiable information.

When such information is not necessary for demonstrating the technical functionality, it can be anonymized.

For example:

```text
192.168.X.X
HOSTNAME
USER
REDACTED
```

This allows the technical evidence to remain useful without exposing unnecessary information.

---

# 29. Final Results

At the end of the project, the laboratory provided a functional centralized security monitoring environment.

The following capabilities were successfully implemented and/or tested:

* Wazuh Server;
* Wazuh Indexer;
* Wazuh Dashboard;
* Windows 10 monitoring;
* Kali Linux monitoring;
* Wazuh Agents;
* Sysmon telemetry;
* Auditd telemetry;
* File Integrity Monitoring;
* Endpoint inventory;
* Vulnerability Detection;
* MITRE ATT&CK visibility;
* Controlled network reconnaissance;
* Security event investigation;
* SIEM troubleshooting.

The laboratory therefore provided practical experience with multiple components of a defensive security infrastructure.

---

# 30. Skills Developed

The project provided practical experience in several cybersecurity domains.

## Security Operations

* Security monitoring;
* Alert analysis;
* Event investigation;
* Log analysis;
* Initial triage.

## SIEM

* Wazuh deployment;
* Agent management;
* Event collection;
* Security rules;
* Alert analysis;
* Dashboard investigation.

## Endpoint Security

* Windows monitoring;
* Linux monitoring;
* Sysmon;
* Auditd;
* File Integrity Monitoring.

## Threat Detection

* Network reconnaissance;
* Security event analysis;
* MITRE ATT&CK;
* Suspicious activity investigation.

## Infrastructure

* Linux server administration;
* Virtualization;
* Network configuration;
* Client-server communication;
* Service troubleshooting.

---

# 31. Conclusion

This project resulted in a functional **Wazuh-based SOC/SIEM laboratory** designed to simulate real-world security monitoring activities.

The implementation started with the deployment of Ubuntu Server 24.04 and the installation of the Wazuh infrastructure.

Windows 10 and Kali Linux were then configured as monitored endpoints using Wazuh Agents.

The environment was enhanced with **Sysmon on Windows** and **Auditd on Kali Linux**, providing additional endpoint telemetry for security analysis.

Additional Wazuh capabilities, including **File Integrity Monitoring, Endpoint Inventory, Vulnerability Detection, and MITRE ATT&CK visibility**, were also explored.

Finally, controlled security activity was generated from Kali Linux using Nmap to validate the monitoring pipeline.

The complete process demonstrated the following security monitoring lifecycle:

```text
COLLECT
   ↓
PROCESS
   ↓
DETECT
   ↓
ALERT
   ↓
INVESTIGATE
   ↓
ANALYZE
   ↓
RESPOND
```

The laboratory therefore provided practical experience with technologies and concepts directly related to:

* **SOC Analyst**
* **Blue Team**
* **SIEM**
* **Security Monitoring**
* **Endpoint Security**
* **Threat Detection**
* **Incident Investigation**

---

# 32. References

The technical information used in this project was based primarily on official and specialized documentation.

## Wazuh

* Wazuh Official Documentation
* Wazuh Architecture Documentation
* Wazuh Components Documentation
* Wazuh Dashboard Documentation
* Wazuh File Integrity Monitoring Documentation
* Wazuh Vulnerability Detection Documentation

## Microsoft

* Microsoft Sysinternals Sysmon Documentation

## Linux

* Linux Audit / Auditd Documentation

## MITRE

* MITRE ATT&CK Framework
