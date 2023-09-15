---
description: Installing an agent onto a device on the network
---

# Installing an Agent

Within the Wazuh Dashboard - add agent.&#x20;

![](<../.gitbook/assets/image (6).png>)

Select the operating system of the host that will be installing the Wazuh agent.&#x20;

![](<../.gitbook/assets/image (7).png>)

Wazuh also offers support for the following operating systems:&#x20;

![](<../.gitbook/assets/image (8).png>)

Next, enter the IP address or the FQDN of the host that will be installing the wazuh agent.&#x20;

![](<../.gitbook/assets/image (10).png>)

Assign an agent name to the host and apply group

![](<../.gitbook/assets/image (11).png>)

Next run the following command to install and enroll the wazuh agent on the linux host machine.

Make sure that the command is run as sudo.&#x20;

`sudo curl -so wazuh-agent.deb https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.5.2-1_amd64.deb && sudo WAZUH_MANAGER='192.168.50.241' WAZUH_AGENT_GROUP='HomeNetwork' WAZUH_AGENT_NAME='Web-Application-Server-StudentWellness' dpkg -i ./wazuh-agent.deb`

To start the agent run the following commands

`sudo systemctl daemon-reload`

`sudo systemctl enable wazuh-agent`

`sudo systemctl start wazuh-agent`



For windows hosts, you will need adminstrator prvilieges to perform the installation in addition to needing PowerShell 3.0 or greater.&#x20;

`Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.5.2-1.msi -OutFile ${env:tmp}\wazuh-agent.msi; msiexec.exe /i ${env:tmp}\wazuh-agent.msi /q WAZUH_MANAGER='192.168.50.241' WAZUH_REGISTRATION_SERVER='192.168.50.241' WAZUH_AGENT_GROUP='HomeNetwork' WAZUH_AGENT_NAME='Dell-XPS'`

![](https://lh5.googleusercontent.com/gNVquC4aJUd\_5wOq53zVXo-NO6hrUvf4VBrFYsrouYFSh3MVZcth8f0U4AHe9HCzp-QnrLFUmC0Zn4eD9-M4sTkiqyGbBKNoIhKUx2tXGJggCVyqQtxvs3To-hXWBEeJnygyhxQybsOXQQvJOqn2bK0)

Verifying that the Agents have been installed:&#x20;

![](<../.gitbook/assets/image (13).png>)

Installing a 3rd agent on a web application server

![](<../.gitbook/assets/image (14).png>)



