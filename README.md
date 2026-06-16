# Wazuh-Home-SOC-Lab

## Objective

Home SOC using Wazuh. This project involved building a Security Operations Center (SOC) environment using VirtualBox, Ubuntu Server, Wazuh, and a Windows 11 endpoint. The goal was to gain hands-on experience with SIEM deployment, endpoint monitoring, agent management, log collection, security event analysis, and Security Configuration Assessment (SCA) using Wazuh.

### Skills Learned

* Built a Home SOC using Wazuh and Windows 11.
* Installed and configured a Wazuh Manager on Ubuntu Linux.
* Deployed and enrolled a Windows 11 endpoint into Wazuh.
* Troubleshot agent enrollment, networking, and authentication issues.
* Configured centralized log collection and endpoint monitoring.
* Analyzed security events through the Wazuh Dashboard.
* Performed Security Configuration Assessment (SCA) against a Windows endpoint.
* Validated agent communication and telemetry collection.
* Gained practical experience with SIEM administration and SOC workflows.

### Tools Used

* VirtualBox — Used to create and manage virtual machines.
* Ubuntu Linux VM — Used to host the Wazuh platform.
* Windows 11 VM — Used as the monitored endpoint.
* Linux Terminal — Used for Wazuh administration and troubleshooting.
* PowerShell — Used for agent deployment and endpoint troubleshooting.
* Wazuh Manager — Used as the centralized SIEM platform.
* Wazuh Dashboard — Used for security monitoring and investigations.
* Wazuh Agent — Used to collect endpoint telemetry from Windows 11.
* Security Configuration Assessment (SCA) — Used to evaluate endpoint security posture.

## Steps

### Phase 1: Build Ubuntu Wazuh Server

#### Step 1: Install VirtualBox

Downloaded and installed Oracle VirtualBox to host the virtual SOC environment.

#### Step 2: Download Ubuntu Server

Downloaded Ubuntu Server LTS and prepared it for deployment.

#### Step 3: Create Ubuntu VM

Created an Ubuntu virtual machine using:

* 8GB RAM
* 8 CPUs
* 80GB Storage
* NAT Network Adapter

Installed Ubuntu Server and configured the initial user account.



#### Step 4: Update Ubuntu

Updated all system packages to ensure a stable environment before installing Wazuh.

```bash
sudo apt update
sudo apt upgrade -y
```



---

### Phase 2: Install Wazuh

#### Step 1: Download Wazuh Installer

Downloaded the Wazuh all-in-one installation script.
<img width="1280" height="854" alt="wazuh instalation" src="https://github.com/user-attachments/assets/1d8ff485-0f89-4c80-a885-95022f423ac9" />

```bash
curl -sO https://packages.wazuh.com/4.12/wazuh-install.sh
chmod +x wazuh-install.sh
```

#### Step 2: Install All-in-One Wazuh

Installed:

* Wazuh Manager
* Wazuh Indexer
* Wazuh Dashboard

```bash
sudo ./wazuh-install.sh -a
```



#### Step 3: Save Credentials

Recorded the Wazuh Dashboard credentials generated during installation.

```text
Username: admin
Password: ********
```

#### Step 4: Access Dashboard

Verified successful deployment of the Wazuh Dashboard and logged in through the web interface.
<img width="1280" height="854" alt="Ubuntu is running" src="https://github.com/user-attachments/assets/691f5331-4ffa-4c55-8de6-4219fee3c354" />

```bash
hostname -I
```
---

### Phase 3: Create Windows Endpoint

#### Step 1: Create Windows 11 VM

Created a Windows 11 virtual machine using:

* 8GB RAM
* 4 CPUs
* 50GB Storage

Installed Windows 11 and completed the initial setup.


#### Step 2: Verify Connectivity

Verified communication between the Windows endpoint and Ubuntu Wazuh server using ping and network connectivity tests.


---

### Phase 4: Install Wazuh Agent

#### Step 1: Create Agent

Created a Windows endpoint agent using the Wazuh Manager agent management utility.

```bash
sudo /var/ossec/bin/manage_agents
```



#### Step 2: Generate Agent Key

Generated an authentication key for the Windows endpoint.


#### Step 3: Install Agent

Installed the Wazuh Agent on Windows 11 and configured communication with the Wazuh Manager.


#### Step 4: Troubleshoot Enrollment

Investigated multiple enrollment and connectivity issues involving:

* Network configuration
* Agent authentication
* Version compatibility
* Manager communication

Reviewed:

```text
ossec.log
ossec.conf
client.keys
```



#### Step 5: Configure Agent

Updated the agent configuration to use the correct Wazuh Manager IP address.

```xml
<address>10.0.2.4</address>
```



#### Step 6: Import Agent Key

Imported the generated enrollment key into the Windows endpoint and restarted the Wazuh Agent service.



#### Step 7: Verify Agent Connection

Confirmed successful communication between the endpoint and manager.

```text
Connected to the server
Agent is now online
```



---

### Phase 5: Verify Logs and Monitoring

#### Step 1: Verify Active Agent

Confirmed the Windows endpoint appeared as an active agent within Wazuh.

```bash
sudo /var/ossec/bin/agent_control -l
```
<img width="1531" height="920" alt="Agent connected" src="https://github.com/user-attachments/assets/2393628c-1dfa-4aa1-91e1-1f35aaf8ee33" />


#### Step 2: Review Security Events

Accessed Wazuh Discover and reviewed incoming endpoint telemetry.



#### Step 3: Security Configuration Assessment

Reviewed Security Configuration Assessment (SCA) results generated against the Windows endpoint.



#### Step 4: Dashboard Monitoring

Verified endpoint visibility through the Wazuh Dashboard.


---

### Phase 6: Final Home SOC Architecture

Completed a functioning Home SOC environment consisting of:

* Ubuntu Server
* Wazuh Manager
* Wazuh Dashboard
* Wazuh Indexer
* Windows 11 Endpoint
* Wazuh Agent
* Centralized Log Collection
* Security Configuration Assessment
* Endpoint Monitoring
* Security Event Analysis

The completed Home SOC provides centralized visibility into endpoint activity and serves as a foundation for future enhancements including Sysmon integration, Atomic Red Team testing, custom detection rules, active response, and threat hunting exercises.
