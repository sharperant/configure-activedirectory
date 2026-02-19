<p align="center">
<img width="300" height="168" alt="azurelab" src="https://github.com/user-attachments/assets/cd0a32c5-a273-4a34-9a49-138242c7b8d3" />
</p>
<p>
  
<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />
</p>
<p>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell
<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)</b>
</p>
<p>
<h2>High-Level Deployment and Configuration Steps</h2>
  
- Create Resources
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (myadproject.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create additional users and attempt to log into client-1 with one of the users
</p>
<p>
<h2>Deployment and Configuration Steps</h2>
</p>
<p>
In the Azure portal, I created a Virtual Network (VNet) and subnet to house both my virtual machines. Then I deployed a Windows Server 2022 VM named "DC-1" to act as my Domain Controller, and assigned it a static private IP address.
</p>
<p>

