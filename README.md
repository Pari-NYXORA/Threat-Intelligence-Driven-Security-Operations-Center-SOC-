🛡️ Threat Intelligence Driven Security Operations Center (SOC)

> A hands-on, isolated SOC lab built to simulate the complete security monitoring lifecycle — from attack simulation and endpoint telemetry to detection, investigation and threat-intelligence enrichment.

---

## 📌 Project Overview

This project is a self-hosted Security Operations Center lab designed to reproduce a realistic blue-team workflow inside an isolated virtual environment.

The lab connects:

**Attack Simulation → Endpoint Telemetry → SIEM → Detection Engineering → Investigation → Threat Intelligence → Response**

The main objective is not simply to install security tools, but to demonstrate how security events are generated, collected, detected, investigated and enriched with threat intelligence.

The environment was built using VMware Workstation and isolated using a Host-Only network.

---

## 🎯 Objectives

- Deploy and configure a Wazuh-based SIEM environment.
- Monitor Windows endpoint activity using Sysmon.
- Monitor Linux activity using Auditd and system logs.
- Collect and correlate endpoint security events.
- Develop detection rules mapped to MITRE ATT&CK.
- Use Sigma-style detection logic for detection engineering.
- Integrate MISP for IOC-based threat intelligence enrichment.
- Perform controlled attack simulations from Kali Linux.
- Investigate alerts using process, network and authentication telemetry.
- Perform threat-hunting exercises using collected logs.
- Document investigation and incident-response workflows.
- Maintain evidence through screenshots, logs and investigation reports.

---

# 🏗️ Lab Architecture

```text
                         ┌─────────────────────┐
                         │     Kali Linux      │
                         │   Attack Simulation │
                         │     192.168.56.20   │
                         └──────────┬──────────┘
                                    │
                              Controlled Attack
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │    Windows 11       │
                         │      Victim         │
                         │   192.168.56.10     │
                         │                     │
                         │ Sysmon + Wazuh Agent│
                         └──────────┬──────────┘
                                    │
                              Telemetry
                                    │
                                    ▼
                    ┌────────────────────────────┐
                    │       Wazuh Manager        │
                    │       192.168.56.5         │
                    │                            │
                    │  Decoders + Rules + Alerts │
                    │  SIEM + Dashboard          │
                    └────────────┬───────────────┘
                                 │
                    ┌────────────┴─────────────┐
                    │                          │
                    ▼                          ▼
          ┌──────────────────┐       ┌──────────────────┐
          │    MISP Server   │       │  Wazuh Dashboard │
          │  192.168.56.6    │       │ Visualization &  │
          │                  │       │ Investigation    │
          │ Threat Intel /   │       └──────────────────┘
          │ IOC Enrichment   │
          └──────────────────┘

             ┌─────────────────────┐
             │   Ubuntu Endpoint   │
             │   192.168.56.15     │
             │ Auditd + Wazuh      │
             │ Agent               │
             └─────────────────────┘

        Network: 192.168.56.0/24
        VMware Host-Only / Isolated Lab
