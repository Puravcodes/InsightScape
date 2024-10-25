# InsightScape

## Project Workflow

![alt text](Azure-Diagram.jpg)


## Project Overview
Welcome to **InsightScape**—an all-encompassing solution for monitoring and maintaining Azure resources. Designed to provide a unified framework, InsightScape leverages powerful Azure tools like Azure Monitor, Log Analytics, Application Insights, Network Watcher, Security Center, and Azure Backup. Together, these tools deliver full-spectrum visibility, enhanced security, and optimal performance management for your cloud environment. With InsightScape, you can ensure proactive and efficient resource monitoring and maintenance across every layer of your Azure infrastructure.

- **Programming required?**: ❌ (This project relies mostly on configuration and integration, though an understanding of Kusto Query Language (KQL) is essential for custom monitoring queries.)

## Azure Services Used
- **Azure Monitor**: Monitoring solution to track metrics and logs.
- **Kusto Query Language (KQL)**: Used for writing custom monitoring queries.
- **Azure Application Insights**: For performance monitoring of the WebApp.
- **Azure Network Watcher**: Network monitoring and diagnostics.
- **Azure Security Center**: Evaluates and provides security recommendations.
- **Azure Backup**: Backup and recovery services for Azure VMs.
- **Azure Alerts**: Configured alerts for resource health and other monitoring activities.

## Purpose
The purpose of this project is to validate my hands-on skills in the **Monitor and Maintain Azure Resources** aspect of the **AZ-104 Certification**. The approach was to set up major and commonly used Azure resources and then work with Azure monitoring and security services.

### Step 1: Resources Setup

#### a) Resource Group and VNet Setup
- Created a **Resource Group** named **InsightScape-RG** in the **West US 2** region.
- Created a **Virtual Network (VNet)** named **InsightScape-VNet** with the following subnets:
  - **VM1-Subnet**: `10.1.1.0/24`
  - **VM2-Subnet**: `10.1.2.0/24`

![alt text](<RG 2.png>)
![alt text](<VNet 6.png>)


#### b) Virtual Machines (VMs) and Network Security Groups (NSGs)
- Created a Windows VM named **InsightScape-VM1** and a Linux VM named **InsightScape-VM2** in the **InsightScape-RG**.
  - **InsightScape-VM1** (Windows Server 2019 Datacenter) configured with an NSG allowing inbound **RDP, HTTP, and HTTPS** traffic.
  - **InsightScape-VM2** (Ubuntu 22.04) configured with an NSG allowing inbound **SSH, HTTPS, and HTTP** traffic.
- Updated NSGs:
  - Added an inbound security rule to **InsightScape-VM1-NSG** for allowing **HTTP** traffic.
  - No changes made to **InsightScape-VM2-NSG** as default configurations were sufficient.


![alt text](<VM 5.png>)
![alt text](<VM 9.png>)
![alt text](<NSGs 3.png>)
![alt text](<NSGs 4.png>)


#### c) Web Application Deployment
- Created a **WebApp** named **InsightScape-WebApp** in **InsightScape-RG**.
  - Published an ASP.NET V4.8 sample application.
  - Configured **Application Insights** for monitoring.


<video controls src="2024-10-21 15-58-00-1.mp4" title="Title"></video>


#### d) Blob Storage and Logic App
- Created a **Blob Storage** account named **insightscapestorage** with a container named **files**.
- Configured a **Logic App** named **InsightScape-LogicApp** to trigger when new blobs are added to the container, using access keys for authentication.


![alt text](<Storage Account 5.png>)
![alt text](<Storage Account 6.png>)
![alt text](<Logic App 12.png>)

#### e) Network Monitoring
- Configured **Network Watcher** for packet capture and connection monitoring.
- Verified packet captures by analyzing captured packets in Wireshark.

![alt text](<Networking Resources 3.png>)
![alt text](<Networking Resources 4.png>)
![alt text](<Networking Resources 17.png>)


#### f) Azure Backup
- Created a **Recovery Services Vault** named **InsightScape-Vault**.
- Configured **Azure Backup** for **InsightScape-VM1**.

![alt text](<Azure Backup 4.png>)
![alt text](<Azure Backup 10.png>)
![alt text](<Azure Backup 13.png>)


### Step 2: Azure Monitor Integration

#### 1) Monitoring Setup for Deployed Resources
- Enabled **Azure Monitor Insights** for both VMs, the WebApp, and the Logic App.
- Set up **Alerts** for **High CPU Usage** on **InsightScape-VM1**.

#### 2) Activity Logs, Metrics, and Diagnostic Settings
- Configured **Metrics** for VMs, WebApp, and Logic App.
- Installed **Diagnostics Extensions** on VMs.
- Enabled **Diagnostic Settings** for **WebApp** and **Default Log Analytics Workspace**.

#### 3) Monitor Resource Health
- **Monitored Resource Health** for all major deployed resources (VMs, WebApp, Logic App) using **Azure Monitor**.
- **Virtual Machines**: Accessed **Resource Health** under **Service Health** in Azure Monitor for **InsightScape-VM1** and **InsightScape-VM2** to verify health status.
- **WebApp**: Selected **Website** as the resource type in **Resource Health**. Resolved a **Critical Risk alert** related to Health Check failure by configuring and enabling health check.
- **Logic App**: Verified health using two methods:
  - Checked **Run History** in Development Tools to verify successful runs.
  - Monitored **Actions Failed** metric under **Monitoring** to ensure no failed actions.


![alt text](<Azure Monitor Integration 7.png>)
![alt text](<Azure Monitor Integration 20.png>)
![alt text](<Logic App Diagnostics 3.png>)
![alt text](<Activity Logs.png>)
![alt text](<VM-Diagnostics 2.png>)
![alt text](<WebApp-Diagnostics 4.png>)
![alt text](<WebApp-Resource Health  1.png>)
![alt text](<WebApp-Resource Health  2.png>)


### Step 3: Application Insights
- Monitored **InsightScape-WebApp** using **Application Insights**.
- Analyzed:
  - **Performance**, **Roles**, **Failures**, **User Interactions**, and **Live Metrics**.
- Added **Diagnostics Settings** for **Application Insights**.

![alt text](<Application Insights 2.png>)
![alt text](<Application Insights 3.png>) 
![alt text](<Application Insights 4.png>)


### Step 4: Network Monitoring
- Used **Network Watcher Topology** to analyze the network infrastructure.
- Conducted **NSG Diagnostics** for **InsightScape-VM1** and **InsightScape-VM2**:
  - Verified inbound and outbound rules and used packet capture to assess traffic status.

![alt text](<Network Monitoring 2.png>)
![alt text](<Network Monitoring 9.png>)
![alt text](<Network Monitoring 11.png>)
![alt text](<Network Monitoring 12.png>)


### Step 5: Security & Compliance
- Reviewed security recommendations using **Azure Security Center** and **Microsoft Defender for Cloud**.
- Applied:
  - **VM Patches and Updates**.
  - **Disk Encryption**.
  - Network access restriction for storage accounts using **Virtual Network Rules**.
- Verified security alerts, ensuring no critical issues.

![alt text](<Security & Compliance 1.png>)
![alt text](<Security & Compliance 2.png>)
![alt text](<Security & Compliance 4.png>)
![alt text](<Security & Compliance 5.png>)

### Step 6: Alerts Configuration
- Created alerts for:
  - **Failed RDP Login Attempts** on **InsightScape-VM1**.

![alt text](<Alerts Configurations 1.png>)
![alt text](<Alerts Configurations 4.png>)


### Step 7: Backup and Disaster Recovery
- Deleted **InsightScape-VM1** and successfully restored it using the **Recovery Services Vault**.
- Verified the restored VM to ensure the integrity of the recovery process.

![alt text](<Backup and Disaster Recovery 4.png>)
![alt text](<Backup and Disaster Recovery 9.png>)
![alt text](<Backup and Disaster Recovery 10.png>)
![alt text](<Backup and Disaster Recovery 11.png>)


## Conclusion

The **InsightScape** project successfully showcased a robust integration of monitoring and maintenance features within Azure, leveraging services like **Azure Monitor**, **Log Analytics**, and **Application Insights**. This project offered hands-on experience in constructing and managing a secure, high-performance cloud environment, focusing on key aspects such as **disaster recovery**, **advanced security measures**, and **customizable alert configurations**. By combining these capabilities, InsightScape effectively demonstrated comprehensive resource visibility, proactive threat management, and enhanced resilience in Azure cloud infrastructure.

## Skills Demonstrated
- **Monitoring and Maintenance**  
  - Employed **Azure Monitor** and **Log Analytics** for in-depth resource tracking and analytics, ensuring comprehensive visibility and optimized performance management.

- **Network Security**  
  - Set up **Network Watcher** diagnostics and **Network Security Groups (NSGs)** to enhance secure network connectivity and enable precise traffic control across resources.

- **Security and Compliance**  
  - Used **Azure Security Center** to bolster the security posture of resources, applying best practices and continuous compliance monitoring to reduce vulnerabilities.

- **Backup and Disaster Recovery**  
  - Configured **Azure Backup** and successfully validated disaster recovery protocols for Azure VMs, ensuring data resilience and business continuity.

- **Alerts Configuration**  
  - Designed proactive alerting mechanisms for real-time monitoring and rapid response, empowering efficient incident management and minimizing downtime.


## Repository Contents
- **Manual**  
  - A comprehensive manual outlining each phase of the project, including step-by-step configurations, monitoring tips, and best practices for seamless implementation.

- **Screenshots**  
  - Visual documentation capturing key stages and configurations throughout the project, organized and stored in the `Screenshots` folder.

- **Source Code**  
  - Contains all scripts and commands used in the project, systematically arranged in the `Source_Code` folder for easy reference and reuse.


"# InsightScape" 
