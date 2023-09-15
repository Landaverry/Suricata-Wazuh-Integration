---
description: Installing JSON viewer on to be able to read Suricata JSON logs.
---

# Installing JSON Viewed

Trying to read JSON file formats normally results in an unreadable view

![](<../.gitbook/assets/image (41).png>)

To work around this the JSON command line processing tool must be installed to help digest this log.&#x20;

Use the following command to instal JQ

```
sudo apt-get install jq
```

![](<../.gitbook/assets/image (42).png>)

This package will essentially allow us to read JSON files in a more readble format

By using the tail command in conjunction with piping the output through the JQ utility we can parse out the previously unreadable text to legible JSON

```
sudo tail -f /var/log/suricata/eve.json | jq 'select(.event_type=="alert")'
```

This command is going to display the latest event logged but can also be used with cat to display all the events captured within the log.&#x20;

![](<../.gitbook/assets/image (43).png>)

