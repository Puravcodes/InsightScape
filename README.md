# InsightScape

## Project Workflow

<div align="center" > 
![Azure-Diagram](https://github.com/user-attachments/assets/bd9c01ff-1e70-425c-b2c6-bf1d954222bc)
</div>


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

![RG 2](https://github.com/user-attachments/assets/fa5b63a1-e562-4140-9fd9-99bbd243cbf1)
![VNet 6](https://github.com/user-attachments/assets/eefd98fb-9d58-4e68-8531-d4a0eaa6e43c)



#### b) Virtual Machines (VMs) and Network Security Groups (NSGs)
- Created a Windows VM named **InsightScape-VM1** and a Linux VM named **InsightScape-VM2** in the **InsightScape-RG**.
  - **InsightScape-VM1** (Windows Server 2019 Datacenter) configured with an NSG allowing inbound **RDP, HTTP, and HTTPS** traffic.
  - **InsightScape-VM2** (Ubuntu 22.04) configured with an NSG allowing inbound **SSH, HTTPS, and HTTP** traffic.
- Updated NSGs:
  - Added an inbound security rule to **InsightScape-VM1-NSG** for allowing **HTTP** traffic.
  - No changes made to **InsightScape-VM2-NSG** as default configurations were sufficient.



![VM 5](https://github.com/user-attachments/assets/c0145da0-9ad2-4962-8e8c-f07c378983af)
![VM 9](https://github.com/user-attachments/assets/761f526e-2a8c-426e-84a1-dfdcf6885289)
![NSGs 3](https://github.com/user-attachments/assets/a16c2911-bdbd-442e-b150-570cda4f7e42)
![NSGs 4](https://github.com/user-attachments/assets/29ddf1c7-4d63-4c64-99a0-9c999a8e7c26)



#### c) Web Application Deployment
- Created a **WebApp** named **InsightScape-WebApp** in **InsightScape-RG**.
  - Published an ASP.NET V4.8 sample application.
  - Configured **Application Insights** for monitoring.



https://github.com/user-attachments/assets/740ed059-5933-41da-a7f0-b4375949997f





#### d) Blob Storage and Logic App
- Created a **Blob Storage** account named **insightscapestorage** with a container named **files**.
- Configured a **Logic App** named **InsightScape-LogicApp** to trigger when new blobs are added to the container, using access keys for authentication.


![Storage Account 5](https://github.com/user-attachments/assets/764e5c7f-833c-4908-87c8-9cefaad2f90b)
![Storage Account 6](https://github.com/user-attachments/assets/cafce490-049e-413e-943f-246262f402b3)
![Logic App 12](https://github.com/user-attachments/assets/faa562ab-97cf-492d-a3b6-5a115dbe1bb6)



#### e) Network Monitoring
- Configured **Network Watcher** for packet capture and connection monitoring.
- Verified packet captures by analyzing captured packets in Wireshark.

![Networking Resources 3](https://github.com/user-attachments/assets/e719789c-8453-4233-800a-93bacc198919)
![Networking Resources 4](https://github.com/user-attachments/assets/7fd4bed7-c2db-4321-a963-13d1198720ff)
![Networking Resources 17](https://github.com/user-attachments/assets/eae0ee2a-34f4-4706-8a87-83d503e31673)




#### f) Azure Backup
- Created a **Recovery Services Vault** named **InsightScape-Vault**.
- Configured **Azure Backup** for **InsightScape-VM1**.

![Azure Backup 4](https://github.com/user-attachments/assets/08272cb2-9d24-4801-9e6f-607e9919a359)
![Azure Backup 10](https://github.com/user-attachments/assets/477cc0e1-2907-4a2c-af03-0a339fa30548)
![Azure Backup 13](https://github.com/user-attachments/assets/752602c7-7005-4f3e-a852-0a146b53b3a2)



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

![Azure Monitor Integration 7](https://github.com/user-attachments/assets/f1d19f90-115d-45ca-bea0-168087d9d20c)
l![Azure Monitor Integration 20](https://github.com/user-attachments/assets/91fc400d-2bc9-4f2a-bf49-f68dc8ff798a)
![Logic App Diagnostics 3](https://github.com/user-attachments/assets/5fa956da-b143-4588-9571-4f4ffabc1c1e)
![Activity Logs](https://github.com/user-attachments/assets/bc647638-4f1f-4b5a-b991-628617c91475)
![VM-Diagnostics 2](https://github.com/user-attachments/assets/6ee0ca10-f855-4275-ac0a-7f696f4f8d57)
![WebApp-Diagnostics 4](https://github.com/user-attachments/assets/d9483e7e-5f81-4b32-bb36-50ac4106981a)
![WebApp-Resource Health  1](https://github.com/user-attachments/assets/22745431-1fde-49fb-8264-869b287a2f3c)
![WebApp-Resource Health  2](https://github.com/user-attachments/assets/b6a825f4-3025-4d01-845e-3ee52d89fc2f)



### Step 3: Application Insights
- Monitored **InsightScape-WebApp** using **Application Insights**.
- Analyzed:
  - **Performance**, **Roles**, **Failures**, **User Interactions**, and **Live Metrics**.
- Added **Diagnostics Settings** for **Application Insights**.

![Application Insights 2](https://github.com/user-attachments/assets/294eaf0c-d4d7-4478-83f7-bae147d6bb1d)
![Application Insights 3](https://github.com/user-attachments/assets/02479353-5328-4e6d-974a-2e45fdf43019)
![Application Insights 4](https://github.com/user-attachments/assets/dc2dafaa-8626-472a-a634-db7b31eb019b)




### Step 4: Network Monitoring
- Used **Network Watcher Topology** to analyze the network infrastructure.
- Conducted **NSG Diagnostics** for **InsightScape-VM1** and **InsightScape-VM2**:
  - Verified inbound and outbound rules and used packet capture to assess traffic status.

![Network Monitoring 2](https://github.com/user-attachments/assets/40bd35c2-1086-49de-8801-4231de5d156c)
![Network Monitoring 9](https://github.com/user-attachments/assets/53e064d5-ea92-4b26-9a73-bb0b980a2837)
![Network Monitoring 11](https://github.com/user-attachments/assets/95517ac3-2b45-4c4e-8aad-58108ec0bec8)
![Network Monitoring 12](https://github.com/user-attachments/assets/5e1ab52d-3492-4fbc-8c53-676a40994d05)




### Step 5: Security & Compliance
- Reviewed security recommendations using **Azure Security Center** and **Microsoft Defender for Cloud**.
- Applied:
  - **VM Patches and Updates**.
  - **Disk Encryption**.
  - Network access restriction for storage accounts using **Virtual Network Rules**.
- Verified security alerts, ensuring no critical issues.

![Security   Compliance 1](https://github.com/user-attachments/assets/398d850c-f244-4490-a3c3-f22377724ff8)
![Security   Compliance 2](https://github.com/user-attachments/assets/8ad15c4a-b540-4349-9cbf-06c3746f06d7)
![Security   Compliance 4](https://github.com/user-attachments/assets/57e73f57-7823-4d12-b01c-24c6cad585e6)
![Security   Compliance 5](https://github.com/user-attachments/assets/bc803874-ae27-4adc-abca-24355cfa82f6)



### Step 6: Alerts Configuration
- Created alerts for:
  - **Failed RDP Login Attempts** on **InsightScape-VM1**.

![Alerts Configurations 1](https://github.com/user-attachments/assets/c5f79f28-b381-408d-b79e-e5312fc90ca3)
![Alerts Configurations 4](https://github.com/user-attachments/assets/c690eacd-f14e-4b1e-9a9d-33239ca9e346)



### Step 7: Backup and Disaster Recovery
- Deleted **InsightScape-VM1** and successfully restored it using the **Recovery Services Vault**.
- Verified the restored VM to ensure the integrity of the recovery process.

![Backup and Disaster Recovery 4](https://github.com/user-attachments/assets/72621ede-b57d-4c81-be2d-314af6b9b02e)
![Backup and Disaster Recovery 9](https://github.com/user-attachments/assets/d6f3f584-f8e2-4aa8-92a7-9b06ac3f5f90)
![Backup and Disaster Recovery 10](https://github.com/user-attachments/assets/28a420f9-29fc-4bed-97cf-36a8e81e71c0)
![Backup and Disaster Recovery 11](https://github.com/user-attachments/assets/0fdf6f4a-ef7e-4210-9c18-9d238014dce7)


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

