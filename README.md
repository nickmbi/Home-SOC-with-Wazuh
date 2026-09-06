# Wazuh Home SOC Lab

## Overview

Built a Home Security Operations Center using VirtualBox, Kali Linux, Ubuntu Server, Wazuh, Microsoft Sysmon, and a Windows 11 endpoint. The project focused on deploying a SIEM, monitoring endpoint activity, collecting Windows security logs, integrating Sysmon telemetry, and analyzing security events through the Wazuh Dashboard.


## Lab Architecture

```text
                    Internet
                       │
                      NAT
                       │
                ┌──────▼──────┐
                │ Kali Linux  │
                │ 10.0.2.15   │
                │             │
                │192.168.50.10│
                └──────┬──────┘
                       │
                 HomeSOC LAN
              192.168.50.0/24
                  │         │
          ┌───────▼───┐ ┌──▼──────────┐
          │ Windows 11│ │ Ubuntu      │
          │ .50.20    │ │ .50.30      │
          │           │ │             │
          │ Wazuh     │ │ Wazuh       │
          │ Agent     │ │ Manager     │
          │ Sysmon    │ │ Dashboard   │
          └───────────┘ └─────────────┘
```


## Tools Used

- VirtualBox
- Ubuntu Linux
- Kali Linux
- Windows 11
- Wazuh
- Sysmon
- Linux Terminal
- PowerShell


## 1. Built the Wazuh Server

Installed Ubuntu Server in VirtualBox.

Updated the operating system.

```bash
sudo apt update
sudo apt upgrade -y
```

Installed the Wazuh platform.

```bash
curl -sO https://packages.wazuh.com/4.12/wazuh-install.sh
chmod +x wazuh-install.sh

sudo ./wazuh-install.sh -a
```

Verified the Wazuh Dashboard was accessible.

<img width="1280" height="854" alt="Ubuntu is running" src="https://github.com/user-attachments/assets/f293a316-5ad2-4191-b3f4-2e0d8e217412" />



## 2. Created the Windows Endpoint

Installed Windows 11 in VirtualBox.

Verified network connectivity between Windows and Ubuntu.



## 3. Installed the Wazuh Agent

Created a Windows endpoint agent.

```bash
sudo /var/ossec/bin/manage_agents
```

Generated and imported the enrollment key.

Configured the agent to communicate with the Wazuh Manager.

Troubleshot enrollment and connectivity issues involving:

- Network configuration
- Agent authentication
- Manager communication

Reviewed:

```text
ossec.log
ossec.conf
client.keys
```

Updated the agent configuration.

```xml
<address>**.*.*.*</address>
```

Verified the agent successfully connected.

<img width="1531" height="920" alt="Agent connected" src="https://github.com/user-attachments/assets/ea2d8546-ce01-4417-9786-cb62bc21f52e" />



## 4. Installed Sysmon

Downloaded Sysmon.

Installed Sysmon on the Windows endpoint.

<img width="1024" height="822" alt="Starting sysmon" src="https://github.com/user-attachments/assets/1af7024d-5545-442f-8771-47894d3247f4" />

Verified Sysmon was generating Windows security events.



## 5. Configured Sysmon Log Collection

Updated the Wazuh Agent configuration to collect Sysmon Operational logs.

Restarted the Wazuh Agent.

Verified Sysmon events were forwarded to the Wazuh Manager.

<img width="1920" height="1005" alt="sysmon events are reaching wazuh" src="https://github.com/user-attachments/assets/62bf6c2a-d348-489c-acbe-7201b3350471" />


## 6. Verified Monitoring

Confirmed the Windows endpoint appeared as an active agent.

Reviewed Windows Event Logs and Sysmon events in the Wazuh Dashboard.

Generated PowerShell activity to confirm endpoint telemetry was being collected.



## 7. Connected Kali Linux

Configured Kali Linux as the security testing machine within the HomeSOC LAN.

Verified Kali Linux could communicate with the Windows 11 endpoint and Ubuntu Wazuh server.

Tested connectivity using:

```bash
ping 192.168.50.20
ping 192.168.50.30
```

Verified the network configuration and IP address:

```bash
ip addr
```

# Skills Learned

- SIEM Deployment
- Linux Administration
- Windows Administration
- Sysmon Deployment
- Windows Event Collection
- Network Troubleshooting
