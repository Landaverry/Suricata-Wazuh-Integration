---
description: >-
  This portion of the project covers integrating Suricata with Wazuh for log
  processing.
---

# Configuring Log Processing

If not already done so, make sure that the machine that will be passing along its suricata IDS logs to Wazuh already has a Wazuh agent installed. The following steps will edit the wazuh configuration from the agent machine side.&#x20;

![](<../.gitbook/assets/image (44).png>)

Next we need to edit the ossec.conf file found on the machine with the agent installed:&#x20;

```
sudo vim /var/ossec/etc/ossec.conf
```

We are looking for the Log Analysis portion of the configuration file. This is where we will configure the wazuh agent to pass along the Suricata log files.&#x20;

![](<../.gitbook/assets/image (45).png>)

The following was added to the Log Analysis portion of the configuration file:&#x20;

`<localfile>`

`<log_format>syslog</log_format>`

`<location>/var/log/suricata/eve.json</location>`

`</localfile>`

![](<../.gitbook/assets/image (47).png>)

Make sure to restart the Wazuh-agent service.&#x20;

![](<../.gitbook/assets/image (46).png>)



Go back to the Wazuh Dashboard:&#x20;

Go to Management > Configuration

![](<../.gitbook/assets/image (48).png>)

Edit the Wazuh Manager Configuration - Here we are looking to add the same configuration that was added to the agent machine.&#x20;

![](<../.gitbook/assets/image (49).png>)

![](<../.gitbook/assets/image (50).png>)

Save and restart the Wazuh Manager.&#x20;

Once restarted, you can then go to the Security Events and filter to the machine that has suricata installed.&#x20;

Testing another ICMP ping to the machine it can be viewed within the Security Alerts.&#x20;

![](<../.gitbook/assets/image (51).png>)

You can also filter by rule groups:&#x20;

![](<../.gitbook/assets/image (52).png>)

Resulting in the following view:&#x20;

![](<../.gitbook/assets/image (53).png>)

JSON Output via Wazuh:&#x20;

```
{
  "agent": {
    "ip": "192.168.50.130",
    "name": "Kali-Linux",
    "id": "001"
  },
  "manager": {
    "name": "wazuh-server"
  },
  "data": {
    "icmp_type": "0",
    "in_iface": "eth0",
    "src_ip": "192.168.50.130",
    "src_port": "0",
    "community_id": "1:IaBY7JTIEOd4nxV6oxx+XVHwAZ8=",
    "event_type": "alert",
    "alert": {
      "severity": "3",
      "signature_id": "1",
      "rev": "1",
      "gid": "1",
      "signature": "ICMP Ping",
      "action": "allowed"
    },
    "flow_id": "1580300367561182.000000",
    "dest_ip": "192.168.50.172",
    "proto": "ICMP",
    "icmp_code": "0",
    "dest_port": "0",
    "pkt_src": "wire/pcap",
    "flow": {
      "src_ip": "192.168.50.172",
      "pkts_toserver": "1",
      "dest_ip": "192.168.50.130",
      "start": "2023-09-14T20:32:05.367942-0400",
      "bytes_toclient": "98",
      "bytes_toserver": "98",
      "pkts_toclient": "1"
    },
    "timestamp": "2023-09-14T20:32:05.367960-0400",
    "direction": "to_client"
  },
  "rule": {
    "firedtimes": 2,
    "mail": false,
    "level": 3,
    "description": "Suricata: Alert - ICMP Ping",
    "groups": [
      "ids",
      "suricata"
    ],
    "id": "86601"
  },
  "decoder": {
    "name": "json"
  },
  "input": {
    "type": "log"
  },
  "@timestamp": "2023-09-15T00:32:41.504Z",
  "location": "/var/log/suricata/eve.json",
  "id": "1694737961.118321",
  "timestamp": "2023-09-15T00:32:41.504+0000",
  "_id": "U9dBlooB8P6HoAuJGYH_"
}
```

Table format:

![](<../.gitbook/assets/image (54).png>)

Testing the testmyids.org command again to confirm visibility in Wazuh:&#x20;

![](<../.gitbook/assets/image (55).png>)

![](<../.gitbook/assets/image (56).png>)
