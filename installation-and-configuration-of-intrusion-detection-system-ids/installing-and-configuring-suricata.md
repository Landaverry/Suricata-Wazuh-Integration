---
description: >-
  This will be based on the host machine that yo will be installing Suricata. It
  is best to follow the documentation listed on their website.
---

# Installing & Configuring Suricata

Suricata Documentation- [https://docs.suricata.io/en/latest/install.html#binary-packages](https://docs.suricata.io/en/latest/install.html#binary-packages)

![](<../.gitbook/assets/image (21).png>)

Enable Suricata to run on startup

```
sudo systemctl enable suricata
```

![](<../.gitbook/assets/image (22).png>)

Modify the Suricata config file to set network ip address and network interfaces to monitor

```
sudo vim /etc/suricata/suricata.yaml
```

![](<../.gitbook/assets/image (23).png>)

![](<../.gitbook/assets/image (24).png>)

Next the comunity-id setting should be modified this will be used for event correlation and useful when using zeek or importing logs in JSON format.&#x20;

Set this option to true.&#x20;

![](<../.gitbook/assets/image (25).png>)



If custom rules need to be specified within Suricata, the path can be specified within this configuration file.&#x20;

![](<../.gitbook/assets/image (26).png>)



**Update the Suricata rulesets:**

```
sudo suricata-update
```

![](<../.gitbook/assets/image (27).png>)

Suricata will then perform a configuration test to ensure there are no errors within the configuration file.&#x20;

![](<../.gitbook/assets/image (28).png>)

Verify that rules have been imported.&#x20;

```
sudo ls -al /var/lib/suricata/rules/
```

![](<../.gitbook/assets/image (29).png>)

Suricata also allows you to select your own sources - This allows you to retrieve your own rulesets from open source or from commercially available products - This products will require a subscription.&#x20;

```
sudo suricata-update list-sources
```

![](<../.gitbook/assets/image (30).png>)

Enable a source:

```
sudo suricata-update enable-source [List Source]
```

![](<../.gitbook/assets/image (31).png>)

Make sure to update suricata to ensure the most up to date rules are pulled.&#x20;



Mannually test that the suricata configuration file works.&#x20;

```
sudo suricata -T -c /etc/suricata/suricata.yaml
```

![](<../.gitbook/assets/image (33).png>)

**Start Suricata:**

```
sudo systemctl start suricata.service
```

Verify that Suricata is running:&#x20;

![](<../.gitbook/assets/image (34).png>)



A quick test to ensure that Suricata is working:

```
curl http://testmynids.org/uid/index.html
```

![](<../.gitbook/assets/image (35).png>)

Verify that this network traffic was logged within suricata's log

```
sudo cat /var/log/suricata/fast.log
```

![](<../.gitbook/assets/image (36).png>)

