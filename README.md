# azure-honeypot-lab
Azure Honeypot project using Microsoft Sentinel and KQL to visualize brute-force attacks

# 🕵️‍♂️ Azure Honeypot and Attack Map Project

## 📘 Overview
This project shows how I created a **honeypot virtual machine in Azure**, captured attacker login attempts, sent logs to **Microsoft Sentinel**, and visualized global attack data on a live map using **KQL queries**.

---

## 🧱 What I Did
1. Created an Azure Virtual Machine and allowed all inbound traffic.
2. Turned off the firewall so attackers could try to connect.
3. Failed a few logins manually to generate Event ID 4625 (failed login).
4. Set up a **Log Analytics Workspace** and **Sentinel** to collect the logs.
5. Imported a **GeoIP watchlist** to add country and city data to attacker IPs.
6. Created a **Sentinel workbook (map)** to visualize attacks on a world map.

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

## 🧑‍💻 Author
**Bharath Y**  
*Aspiring Cybersecurity Analyst | Cloud Security Enthusiast*  
[LinkedIn Profile](https://linkedin.com/in/your-link) | [GitHub Profile](https://github.com/yourusername)

