# Laboratory Findings

## Overview

The laboratory successfully demonstrated centralized security
monitoring using Wazuh across Windows and Linux endpoints.

## Key Findings

### Endpoint Monitoring

Windows 10 and Kali Linux endpoints were successfully registered and
monitored by the Wazuh Manager.

### Windows Telemetry

Sysmon provided additional endpoint telemetry that could be analyzed
through the Wazuh platform.

### Linux Auditing

Auditd events were collected from the Kali Linux endpoint and made
available for security analysis.

### File Integrity Monitoring

FIM provided visibility into monitored file changes.

### Vulnerability Detection

The Wazuh vulnerability detection capability identified vulnerabilities
associated with monitored software packages.

### Network Activity

Controlled Nmap activity was generated from the Kali Linux endpoint and
investigated through the Wazuh environment.

### MITRE ATT&CK

Relevant security events were contextualized using MITRE ATT&CK
techniques available through Wazuh.

## Conclusion

The laboratory successfully demonstrated the core workflow of a
security monitoring environment:

Event Generation
→ Collection
→ Detection
→ Visualization
→ Investigation
