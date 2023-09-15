---
description: >-
  Installation and configuration process for deploying Suricata IDS in home
  network. The configuration of the IDS aims to feed the logs of several VMs
  into the Wazuh SIEM for analysis
---

# Installation and Configuration of Intrusion Detection System (IDS)

Suricata is a free open-source threat detection engine and is owned and developed by the community-run non-profit OSIF.&#x20;

Github Repo: [https://github.com/OISF/suricata](https://github.com/OISF/suricata)

Suricata has two main operational modes:&#x20;

* Active (IPS) - Used to alert, log, and block network traffic that matches specific rules.&#x20;
* Passive (IDS) Used to Identify, alert, and log suspicious network traffic within a network.&#x20;

In this project Suricata will be deployed in IDS mode on the network to monitor network traffic. Suricata uses a set of pre-defined rules to identify malicious traffic, once malicious traffic is detected and is matched against a rule set an alert is generated and the traffic is logged.&#x20;

Suricata is very similar to Snort, both logs can be imported or relayed to a SIEM. This project intends to import Suricata Logs into the Wazuh SIEM for live security event monitoring.&#x20;

