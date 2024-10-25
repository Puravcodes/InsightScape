# InsightScape

## Project Workflow

![Azure-Diagram](https://github.com/user-attachments/assets/2819a13f-3b8c-49b6-aba7-f64328b6e928)



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


![RG 2](https://github.com/user-attachments/assets/79cc0bfd-507e-48cf-a696-6de73c31bb2f)
![VNet 6](https://github.com/user-attachments/assets/2f58bfde-bcb0-4933-86bb-f9f842078a53)


#### b) Virtual Machines (VMs) and Network Security Groups (NSGs)
- Created a Windows VM named **InsightScape-VM1** and a Linux VM named **InsightScape-VM2** in the **InsightScape-RG**.
  - **InsightScape-VM1** (Windows Server 2019 Datacenter) configured with an NSG allowing inbound **RDP, HTTP, and HTTPS** traffic.
  - **InsightScape-VM2** (Ubuntu 22.04) configured with an NSG allowing inbound **SSH, HTTPS, and HTTP** traffic.
- Updated NSGs:
  - Added an inbound security rule to **InsightScape-VM1-NSG** for allowing **HTTP** traffic.
  - No changes made to **InsightScape-VM2-NSG** as default configurations were sufficient.


![VM 5](https://github.com/user-attachments/assets/155ea686-41d2-4d7a-89d1-24d6bc1088c5)
![VM 9](https://github.com/user-attachments/assets/abab3cbf-d213-4e37-9086-078b827e6b6d)
![NSGs 3](https://github.com/user-attachments/assets/faf67b1f-b043-4087-996c-17022b127943)
![NSGs 4](https://github.com/user-attachments/assets/6a1f4d9e-e711-48c3-8592-9ca89842b069)



#### c) Web Application Deployment
- Created a **WebApp** named **InsightScape-WebApp** in **InsightScape-RG**.
  - Published an ASP.NET V4.8 sample application.
  - Configured **Application Insights** for monitoring.


https://github.com/user-attachments/assets/881509a2-1422-4f7f-bba1-5dfa367f679e




#### d) Blob Storage and Logic App
- Created a **Blob Storage** account named **insightscapestorage** with a container named **files**.
- Configured a **Logic App** named **InsightScape-LogicApp** to trigger when new blobs are added to the container, using access keys for authentication.


![Storage Account 5](https://github.com/user-attachments/assets/0a29354f-97ef-42f4-9784-118e70093304)
![Storage Account 6](https://github.com/user-attachments/assets/5495fb2f-ed61-42d1-8025-c8329696aca9)
![Logic App 12](https://github.com/user-attachments/assets/783e2e3c-d1b9-4707-8e0c-7253faf62de5)



#### e) Network Monitoring
- Configured **Network Watcher** for packet capture and connection monitoring.
- Verified packet captures by analyzing captured packets in Wireshark.

![alt text](<Networking Resources 3.png>)
![alt text](<Networking Resources 4.png>)
![alt text](<Networking Resources 17.png>)

![Networking Resources 3](https://github.com/user-attachments/assets/352d60a7-5860-424c-bcb9-d7278e48a55d)
![Networking Resources 4](https://github.com/user-attachments/assets/441bd30b-e3ea-4b1b-94d3-63d030b573c2)
![Networking Resources 17](https://github.com/user-attachments/assets/a30e4e37-22a5-4ebb-b748-a427df6b69e3)



#### f) Azure Backup
- Created a **Recovery Services Vault** named **InsightScape-Vault**.
- Configured **Azure Backup** for **InsightScape-VM1**.

![Azure Backup 4](https://github.com/user-attachments/assets/d29c446e-c9fe-4a7c-8386-d157018e631c)
![Azure Backup 10](https://github.com/user-attachments/assets/f387fc7f-01da-4bd1-9658-2cd611d91fd4)
![Azure Backup 13](https://github.com/user-attachments/assets/c38fe098-f433-466c-a1be-c177dafb75cb)



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


![Azure Monitor Integration 7](https://github.com/user-attachments/assets/e5d91f5b-ef35-4379-9f5e-dc27379d95e3)
![Azure Monitor Integration 20](https://github.com/user-attachments/assets/a8ffa9a2-e0fc-465d-b14f-bac0aa02d0a4)
![Logic App Diagnostics 3](https://github.com/user-attachments/assets/43554f85-0d9e-490b-be0c-e9861166d200)
![Activity Logs](https://github.com/user-attachments/assets/5afce28a-ca77-4bb3-a960-4197d5f74893)
![VM-Diagnostics 2](https://github.com/user-attachments/assets/b4ebc055-a113-4261-9276-28cc42b6f9ba)
![WebApp-Diagnostics 4](https://github.com/user-attachments/assets/35c697c9-5afa-44cf-b208-52570890d518)
![WebApp-Resource Health  1](https://github.com/user-attachments/assets/47d0887f-c82e-4792-aeca-ac8c169fff14)
![WebApp-Resource Health  2](https://github.com/user-attachments/assets/f75e1bc9-0f87-49c4-9da5-a807e4b4f180)


### Step 3: Application Insights
- Monitored **InsightScape-WebApp** using **Application Insights**.
- Analyzed:
  - **Performance**, **Roles**, **Failures**, **User Interactions**, and **Live Metrics**.
- Added **Diagnostics Settings** for **Application Insights**.


![Application Insights 2](https://github.com/user-attachments/assets/1d955391-0629-49e2-9752-9de8601dfe37)
![Application Insights 3](https://github.com/user-attachments/assets/42fe47ab-6ea3-4712-a958-1a02575e6f86)
![Application Insights 4](https://github.com/user-attachments/assets/87f7b160-b3a6-4b58-a10b-c4484c826bf1)




### Step 4: Network Monitoring
- Used **Network Watcher Topology** to analyze the network infrastructure.
- Conducted **NSG Diagnostics** for **InsightScape-VM1** and **InsightScape-VM2**:
  - Verified inbound and outbound rules and used packet capture to assess traffic status.

![Network Monitoring 2](https://github.com/user-attachments/assets/b42befd0-b0e9-4bc6-a1da-ca9e5fd2d5bb)
![Network Monitoring 9](https://github.com/user-attachments/assets/ed8aa9fb-4b2c-4abd-8d9c-4bb3b177b386)
![Network Monitoring 11](https://github.com/user-attachments/assets/012f78b2-8089-46f4-926d-8e8618f96c58)
![Network Monitoring 12](https://github.com/user-attachments/assets/9d8c4392-b07b-48e5-b618-15b8987d5c12)




### Step 5: Security & Compliance
- Reviewed security recommendations using **Azure Security Center** and **Microsoft Defender for Cloud**.
- Applied:
  - **VM Patches and Updates**.
  - **Disk Encryption**.
  - Network access restriction for storage accounts using **Virtual Network Rules**.
- Verified security alerts, ensuring no critical issues.

![Security   Compliance 1](https://github.com/user-attachments/assets/62067d14-3a07-4411-8532-d55a0f4c58d9)
![Security   Compliance 2](https://github.com/user-attachments/assets/7c65e290-e9a6-4e00-a889-ba5a91f7aebc)
![Security   Compliance 4](https://github.com/user-attachments/assets/4aab4e45-ecf1-474a-a834-a73d70b52c4c)
![Security   Compliance 5](https://github.com/user-attachments/assets/bc12bf22-9e14-4556-bd61-7e786b442d89)




### Step 6: Alerts Configuration
- Created alerts for:
  - **Failed RDP Login Attempts** on **InsightScape-VM1**.

![Alerts Configurations 1](https://github.com/user-attachments/assets/4b1e4dca-d932-4e32-a7b3-edde1c8776d8)
![Alerts Configurations 4](https://github.com/user-attachments/assets/9e10f6f5-aa2e-4ab2-a9d7-ef6b67a17c39)



### Step 7: Backup and Disaster Recovery
- Deleted **InsightScape-VM1** and successfully restored it using the **Recovery Services Vault**.
- Verified the restored VM to ensure the integrity of the recovery process.

![Backup and Disaster Recovery 4](https://github.com/user-attachments/assets/1f28dfb4-c470-4aec-9bd9-6e8b34a1247b)
![Backup and Disaster Recovery 9](https://github.com/user-attachments/assets/34b5b093-0625-4ddf-9445-dacfc864a54d)
![Backup and Disaster Recovery 10](https://github.com/user-attachments/assets/7301436f-8673-4266-9130-6430df4e505e)
![Backup and Disaster Recovery 11](https://github.com/user-attachments/assets/199ca1ac-821a-4aba-967b-e49ebc2b7574)




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



