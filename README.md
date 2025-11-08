# azure-honeypot-lab
Azure Honeypot project using Microsoft Sentinel and KQL to visualize brute-force attacks

# 🕵️‍♂️ Azure Honeypot and Attack Map Project





## 📘 Overview
This project shows how I created a **honeypot virtual machine in Azure**, captured attacker login attempts, sent logs to **Microsoft Sentinel**, and visualized global attack data on a live map using **KQL queries**.

---

## 🧱 What I Did
### 1. Created an Azure Virtual Machine and allowed all inbound traffic.
- Go to the **Azure Portal** and create a new virtual machine.
- Select **Windows 10** as the operating system.
- Choose an appropriate **VM size** based on your subscription 
- Be aware of the **monthly cost** if the VM runs continuously. Shut it down when not in use.
- If you're using the **Cyber Range**, backend costs are managed for you.
- Set a **username and password**, and make sure to save them securely.
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/083ae42711716c252a71348af3d6bd722e920f00/images/1.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/7033f54bf80c81f44e74373600015050dfbcc567/images/2.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/3.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/5.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/6.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/8.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/10.png)
#### leave default advanced and tags 
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/11.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/Deploying%20vm%2012.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/Successful%20deployment%2013.png)

### 🔐 Step 2: Configure Network Security Group (NSG)

- Go to the **Network Security Group (NSG)** associated with your virtual machine.
- First, **delete the default RDP rule** to remove restricted access.
- Then, create a new **inbound security rule** to allow all traffic.

#### 🔧 Inbound Rule Settings:
- **Source**: Any  
- **Destination**: Any  
- **Protocol**: Any  
- **Port Range**: `*`  
- **Action**: Allow  
- **Priority**: `100` (or any low number to ensure it takes precedence)

> ⚠️ This configuration is intentionally insecure for honeypot purposes. Do not use in production environments.

![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/Deleting%20RDP%20inbound%20rule%2014.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/adding%20inbound%20rule%2015.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/changing%20destination%20port%20ranges%20and%20name%2016.png)
### 🔥 Step 3: Disable Windows Defender Firewall to attract more attackers

- Open your **Windows 10 Virtual Machine** from the Azure Portal.
- Go to **Start Menu** → search for **Windows Defender Firewall** and open it.
- In the left pane, click on **"Advanced Settings"**.
- In the **Windows Defender Firewall with Advanced Security** window:
  
  - Click on **Domain Profile** → set **Firewall state** to **Off**.
    
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/17.png)



  - Click on **Private Profile** → set **Firewall state** to **Off**.
    
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/18.png)


  - Click on **Public Profile** → set **Firewall state** to **Off**.
    
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/19.png)


### 🚫 Step 4: Simulate and Check Failed Login Attempts

- I intentionally tried logging into the VM with incorrect credentials to generate failed login events.
- These attempts helped test the honeypot’s ability to detect unauthorized access.
- To verify the events:
  - Open the **Windows 10 Virtual Machine**.
  - Go to **Start Menu** → search for **Event Viewer** and open it.
  - Navigate to: **Windows Logs** → **Security**
  - Look for entries with **Event ID 4625** — these indicate failed login attempts.
- These logs are forwarded to **Microsoft Sentinel** for further analysis and visualization.

![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/failed%20login%20vm%2021.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/login%20vm%2022%20.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/open%20event%20viewer%2023.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/check%20login%20failer%204625%2025.png)



### 📊 Step 6: Set Up Log Analytics Workspace and Microsoft Sentinel

- First, create a **Log Analytics Workspace** in the Azure Portal.
  - Go to **Monitor** → **Log Analytics Workspaces** → **Create**.
  - Choose a name, resource group, and region.

- After the workspace is created, set up **Microsoft Sentinel**:
  - Go to **Microsoft Sentinel** in the Azure Portal.
  - Click **+ Add** and select the Log Analytics Workspace you just created.
  - Click **Enable** to activate Sentinel on that workspace.

> ✅ This setup is required to collect and analyze logs from your honeypot VM in Sentinel.

![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/create%20log%20analytics%20workspace%2026.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/log%20analytics%20workspace%20created%2027.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/create%20sentinel%2028.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/click%20add%20log%20analytics%20workspace%2030.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/sentinel%20trial%20activated%2031.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/in%20search%20select%20windows%20sec%20event%20and%20click%20manage%2033.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/Select%20win%20sec%20eve%20via%20AMA%20and%20select%20open%20connector%20page%2034.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/click%20create%20data%20collection%20rule%2035%20.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/fill%20creat%20data%20collection%20rule%2036.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/Select%20resources%2037.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/review%20and%20create%2038.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/check%20in%20vm%20azure%20monitor%20created%2039.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/open%20log%20analytics%20workspace%20%2C%20click%20logs%2040.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/run%20query%20secuirty%20event%20id%204625%2041.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/nmap%20scan%20vm%2041.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/nmap%20bruteforce%2042.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/failed%20logins%20from%20different%20accounts%2043.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/run%20query%20check%20-de%20login%20attemps%2044.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/query%20to%20check%20login%20failure%204625.png)
#### instead of adding csv file in watchlist , i checked online
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/53.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/54.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/55.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/click%20chart%20buttton%20in%20logs%20workspace%2057.png)
![Image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/141327cf74335af287208fce931f2692b7dad797/images/attacking%20map.png)
7. Imported a **GeoIP watchlist** to add country and city data to attacker IPs.
8. Created a **Sentinel workbook (map)** to visualize attacks on a world map.

---

## 🧠 Skills Learned
- Azure Virtual Machines  
- Microsoft Sentinel (SIEM)  
- Log Analytics Workspace  
- KQL (Kusto Query Language)  
- Event Viewer and Log Analysis  
- GeoIP Data Enrichment  
- Security Monitoring and Visualization  

---

## 🧰 Tools Used
Azure | Microsoft Sentinel | KQL | Windows 10 | Event Viewer | PowerShell | GeoIP CSV | Log Analytics Workspace

---

## 🖼️ Screenshots
You can see the steps in the screenshots folder:
- VM setup  
- Event Viewer failed logins  
- Sentinel log query  
- GeoIP import  
- Attack Map visualization  

---


