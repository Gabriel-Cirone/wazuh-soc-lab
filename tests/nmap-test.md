# Nmap Detection Test

## Objective

Generate controlled network scanning activity from the Kali Linux
endpoint and evaluate the visibility of the activity through the
Wazuh environment.

## Test Environment

- Source: Kali Linux
- Destination: Wazuh monitored environment
- Monitoring: Wazuh Agent / Wazuh Manager

## Procedure

A controlled Nmap scan was executed from the Kali Linux endpoint.

The purpose was to generate network reconnaissance activity and
evaluate the resulting telemetry.

## Detection Flow

Kali Linux
↓
Nmap
↓
Network Activity
↓
Wazuh Agent
↓
Wazuh Manager
↓
Wazuh Dashboard

## Result

The generated activity was investigated through the Wazuh interface.

