# azure-honeypot-lab
Azure Honeypot project using Microsoft Sentinel and KQL to visualize brute-force attacks

# 🕵️‍♂️ Azure Honeypot and Attack Map Project

## 📘 Overview
This project shows how I created a **honeypot virtual machine in Azure**, captured attacker login attempts, sent logs to **Microsoft Sentinel**, and visualized global attack data on a live map using **KQL queries**.

---

## 🧱 What I Did
### 1. Created an Azure Virtual Machine and allowed all inbound traffic.
       ![image alt](https://github.com/Achyut-Ch/azure-honeypot-lab/blob/main/images/1.png?raw=true)
3. Turned off the firewall so attackers could try to connect.
4. Failed a few logins manually to generate Event ID 4625 (failed login).
5. Set up a **Log Analytics Workspace** and **Sentinel** to collect the logs.
6. Imported a **GeoIP watchlist** to add country and city data to attacker IPs.
7. Created a **Sentinel workbook (map)** to visualize attacks on a world map.

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


