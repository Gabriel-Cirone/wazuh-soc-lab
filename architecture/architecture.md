# Wazuh SOC/SIEM Architecture

```text
                                      ┌──────────────────────────────┐
                                      │       WAZUH DASHBOARD        │
                                      │                              │
                                      │  • Alerts                    │
                                      │  • Events                    │
                                      │  • FIM                       │
                                      │  • Vulnerabilities           │
                                      │  • MITRE ATT&CK              │
                                      │  • Endpoint Monitoring       │
                                      └──────────────┬───────────────┘
                                                     │
                                                     ▼
                                      ┌──────────────────────────────┐
                                      │        WAZUH INDEXER         │
                                      │                              │
                                      │  • Data Storage              │
                                      │  • Event Indexing            │
                                      │  • Search                    │
                                      └──────────────┬───────────────┘
                                                     │
                                                     ▼
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                            UBUNTU SERVER 24.04                                      │
│                                                                                     │
│                              ┌──────────────────────────┐                           │
│                              │      WAZUH SERVER        │                           │
│                              │                          │                           │
│                              │  • Event Processing      │                           │
│                              │  • Decoders              │                           │
│                              │  • Rules                 │                           │
│                              │  • Alert Generation      │                           │
│                              │  • Agent Management      │                           │
│                              └────────────┬─────────────┘                           │
│                                           │                                         │
└───────────────────────────────────────────┼─────────────────────────────────────────┘
                                            │
                           ┌────────────────┴────────────────┐
                           │                                 │
                           ▼                                 ▼
              ┌──────────────────────────┐      ┌──────────────────────────┐
              │        WINDOWS 10        │      │       KALI LINUX         │
              │                          │      │                          │
              │     ┌──────────────┐     │      │     ┌──────────────┐     │
              │     │ Wazuh Agent  │─────┼──────┼────▶│ Wazuh Agent  │     │
              │     └──────────────┘     │      │     └──────────────┘     │
              │            │             │      │            │             │
              │            ▼             │      │            ▼             │
              │     ┌──────────────┐     │      │     ┌──────────────┐     │
              │     │    Sysmon    │     │      │     │    Auditd    │     │
              │     └──────────────┘     │      │     └──────────────┘     │
              │                          │      │            │             │
              │  • Windows Events        │      │     ┌──────────────┐     │
              │  • Process Events        │      │     │     Nmap     │     │
              │  • Network Events        │      │     └──────────────┘     │
              │  • File Activity         │      │            │             │
              └──────────────────────────┘      │  • Linux Audit Events    │
                                                │  • Network Testing       │
                                                └──────────────────────────┘


                              ───────── DATA FLOW ─────────

          WINDOWS 10 ──┐
                        ├──▶ WAZUH AGENT ──▶ WAZUH SERVER ──▶ INDEXER ──▶ DASHBOARD
          KALI LINUX ──┘
