---
description: Create a Custom rule that tracks any ICMP requests to the network
---

# Creating Custom Suricata Rules

Create a rules file with any text editor to either the suricata rules directory or any other directory that you chose.&#x20;

Please keep in mind if you chose to create the rules file in another directory you will have to go to the Suricata configuration and update the rules pathing.&#x20;



```
sudo vim /etc/suricata/rules/local.rules
```

This rule will alert whenever an external connecting device pings the internal network with ICMP pings on any port.&#x20;

```
alert icmp any any -> $HOME_NET any (msg:"ICMP Ping"; sid:1; rev:1;)
```

Formatting for Rules can be found here: [https://docs.suricata.io/en/suricata-6.0.0/rules/intro.html](https://docs.suricata.io/en/suricata-6.0.0/rules/intro.html)

Modifying the yaml configuration file:

![](<../.gitbook/assets/image (37).png>)

Make sure to test the configuration file once the changes has been made:&#x20;

```
sudo suricata -T -c /etc/suricata/suricata.yaml -v
```

![](<../.gitbook/assets/image (38).png>)

Configuration ran successfully.&#x20;

**Testing if rule works:**&#x20;

![](<../.gitbook/assets/image (39).png>)

```
sudo cat /var/log/suricata/fast.log
```

![](<../.gitbook/assets/image (40).png>)

