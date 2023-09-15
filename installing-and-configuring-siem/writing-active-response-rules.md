---
description: Writing Active response rules for brute force attempts
---

# Writing Active Response Rules

Active response rule that takes Failed user login events - rule id 5710 and creates a timeout delay for users who attempt to login with an invalid user account or password&#x20;

```
<active-response>
    <command>firewall-drop</command>
    <location>local</location>
    <rules_id>5710</rules_id>
    <timeout>1000</timeout>
</active-response>
```

Ann attempt was made to SSH into one of the agents using an invalid user&#x20;

![](<../.gitbook/assets/image (18).png>)

On the Wazuh Dahboard the alert was picked up using the above active response rule.&#x20;

![](<../.gitbook/assets/image (19).png>)

![](<../.gitbook/assets/image (20).png>)



JSON output of the Security Alert:&#x20;

```
{
  "predecoder": {
    "hostname": "wazuh-server",
    "program_name": "sshd",
    "timestamp": "Sep 12 22:16:00"
  },
  "agent": {
    "name": "wazuh-server",
    "id": "000"
  },
  "manager": {
    "name": "wazuh-server"
  },
  "data": {
    "srcuser": "user",
    "srcip": "192.168.50.112",
    "srcport": "64509"
  },
  "rule": {
    "mail": false,
    "level": 5,
    "hipaa": [
      "164.312.b"
    ],
    "pci_dss": [
      "10.2.4",
      "10.2.5",
      "10.6.1"
    ],
    "tsc": [
      "CC6.1",
      "CC6.8",
      "CC7.2",
      "CC7.3"
    ],
    "description": "sshd: Attempt to login using a non-existent user",
    "groups": [
      "syslog",
      "sshd",
      "authentication_failed",
      "invalid_login"
    ],
    "nist_800_53": [
      "AU.14",
      "AC.7",
      "AU.6"
    ],
    "gdpr": [
      "IV_35.7.d",
      "IV_32.2"
    ],
    "firedtimes": 1,
    "mitre": {
      "technique": [
        "Password Guessing",
        "SSH",
        "Valid Accounts"
      ],
      "id": [
        "T1110.001",
        "T1021.004",
        "T1078"
      ],
      "tactic": [
        "Credential Access",
        "Lateral Movement",
        "Defense Evasion",
        "Persistence",
        "Privilege Escalation",
        "Initial Access"
      ]
    },
    "id": "5710",
    "gpg13": [
      "7.1"
    ]
  },
  "decoder": {
    "parent": "sshd",
    "name": "sshd"
  },
  "full_log": "Sep 12 22:16:00 wazuh-server sshd[4761]: Invalid user user from 192.168.50.112 port 64509",
  "input": {
    "type": "log"
  },
  "@timestamp": "2023-09-12T22:16:01.663Z",
  "location": "/var/log/secure",
  "id": "1694556961.6950006",
  "timestamp": "2023-09-12T22:16:01.663+0000",
  "_id": "Gtd3i4oB8P6HoAuJWEb1"
}
```

