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
Setup Resources in Azure. In the Azure portal, I created a Virtual Network (VNet) and subnet to house both my virtual machines. Then I deployed a Windows Server 2022 VM named "DC-1" to act as my Domain Controller, and assigned it a static private IP address.
</p>
<p>
<img width="80%" height="560" alt="slide1" src="https://github.com/user-attachments/assets/17fc0484-96a7-4ef7-8077-2c4d5f24b8fd" />
</p>
<p>
<img width="80%" height="560" alt="slide2" src="https://github.com/user-attachments/assets/6a7da878-8bde-48c6-b9b2-9b588c928e47" />
</p>
<p>
I also deployed a Windows 10 VM named "Client-1" in the same VNet, region, and resource group as the domain controller to ensure proper communication between the two machines.
</p>
<p>
<img width="80%" height="561" alt="slide3" src="https://github.com/user-attachments/assets/eada7311-f98a-460b-98d1-53365500ee45" />
</p>
<p>
Set Domain Controller’s NIC Private IP address to be static:
</p>
<p>
<img width="80%" height="565" alt="slide4" src="https://github.com/user-attachments/assets/1a7e7e31-8c0a-4463-be0d-a8967819a739" />
</p>
<p>
<img width="80%" height="563" alt="slide5" src="https://github.com/user-attachments/assets/9f8eb5c0-7644-4f0d-9a1b-1d99d558c33c" />
</p>
<p>
Ensure Connectivity between the client and Domain Controller. To verify network connectivity, I logged into Client-1 using Remote Desktop and continuously pinged DC-1’s private IP using the ping -t command.
</p>
<p>
<img width="80%" height="437" alt="slide6" src="https://github.com/user-attachments/assets/86aa9e2d-0a41-41de-be60-c4c1c62a2085" />
</p>
<p>
I then logged into DC-1 and enabled ICMPv4 (ping) through the local Windows Firewall.
</p>
<p>
<img width="80%" height="562" alt="slide7" src="https://github.com/user-attachments/assets/ac063d96-31ec-4324-a77a-a92249b59022" />
</p>
<p>
I confirmed back on Client-1 that the ping was successful, indicating proper connectivity.
</p>
<p>
<img width="80%" height="445" alt="slide8" src="https://github.com/user-attachments/assets/d769ca3d-7aa6-4256-bb47-2e9309475c35" />
</p>
<p>
Installing Active Directory. Next, I installed Active Directory Domain Services on DC-1 and promoted it to a Domain Controller by creating a new forest called mydomain.com (or myadproject.com).
</p>
<p>
<img width="80%" height="616" alt="slide9" src="https://github.com/user-attachments/assets/c1f20043-806e-4361-a6b6-28cc2f7ecef4" />
</p>
<p>
Promoting it as a Domain Controller
</p>
<p>
<img width="80%" height="620" alt="slide10" src="https://github.com/user-attachments/assets/6a6231bd-5def-48dc-904a-df4ae0f98f97" />
</p>
<p>
<img width="80%" height="618" alt="slide11" src="https://github.com/user-attachments/assets/72a2c733-0a68-466d-9bfd-f58cbe7ef582" />
</p>
<p>
After the system rebooted, I logged into DC-1 using the domain account mydomain.com\labuser.
</p>
<p>
<img width="80%" height="538" alt="slide12" src="https://github.com/user-attachments/assets/83475086-c312-4c97-9429-58a7f6f83f5e" />
</p>
<p>
Create an Admin and Normal User Account in AD. Inside Active Directory Users and Computers (ADUC), I created two Organizational Units (OUs): _EMPLOYEES and _ADMINS.
</p>
<p>
<img width="80%" height="617" alt="slide13" src="https://github.com/user-attachments/assets/ed3534a1-91e9-4a91-b61b-7d5785c28543" />
</p>
<p>
<img width="80%" height="617" alt="slide13" src="https://github.com/user-attachments/assets/2d74d18c-e2a0-4cfe-b947-a359a660f032" />
</p>
<p>
I then created a new user named Jane Doe with the username jane_admin and added her to the “Domain Admins” security group. Afterward, I logged out and logged back into DC-1 using the new admin credentials mydomain.com\jane_admin
</p>
<p>
<img width="80%" height="722" alt="slide15" src="https://github.com/user-attachments/assets/0e24fc14-5017-416c-974e-d9d43642d4ab" />
</p>
<p>
<img width="80%" height="666" alt="slide16" src="https://github.com/user-attachments/assets/2e215efd-2418-4ebb-a6cc-4ee80bebb411" /> 
</p>
<p>
Afterward, I logged out and logged back into DC-1 using the new admin credentials mydomain.com\jane_admin
</p>
<p>
<img width="80%" height="527" alt="slide17" src="https://github.com/user-attachments/assets/aa6e93e1-64ad-4a76-8430-86df839a9e3f" />
</p>
<p>
Join Client-1 to your domain (myadproject.com). From the Azure portal, I changed Client-1's DNS settings to point to DC-1’s private IP address and restarted the VM.
</p>
<p>
<img width="80%" height="560" alt="slide18" src="https://github.com/user-attachments/assets/c39c121c-97ef-4865-a5b7-13e7d2c0bf88" />
</p>
<p>
I then logged into Client-1 as the local admin and joined the computer to the domain mydomain.com.
</p>
<p>
<img width="80%" height="621" alt="slide19" src="https://github.com/user-attachments/assets/fae11a98-5fd7-411d-8838-082a5ffe8c98" />
</p>
<p>
After the machine restarted, I logged into DC-1 and confirmed in ADUC that Client-1 appeared under the “Computers” container, then moved it into the _CLIENTS OU after creating it.
</p>
<p>
<img width="80%" height="625" alt="slide20" src="https://github.com/user-attachments/assets/1881d47e-5f12-4aff-beab-86fb0262d27f" />
</p>
<p>
Enable Remote Desktop Access for Domain Users. While logged into Client-1 as jane_admin, I opened the system settings and enabled Remote Desktop. I then granted the “Domain Users” group permission to access the machine remotely, allowing standard users to log in via RDP. This could also be automated using Group Policy for larger environments.
</p>
<p>
<img width="80%" height="581" alt="slide21" src="https://github.com/user-attachments/assets/3410fdb0-516f-44c6-894f-40ab008d0100" />
</p>
<p>
Bulk Create Users and Configure Lockout Policy. Back on DC-1, I opened PowerShell ISE as an administrator and ran a script to automatically generate 10,000 user accounts inside the _EMPLOYEES OU.I tested account lockout by logging in with incorrect credentials multiple times, causing the account to be locked. I then reset the password and unlocked the account through ADUC. Finally, I modified the domain’s Group Policy settings to lock user accounts after 5 failed login attempts, with a 30-minute lockout duration.
</p>
<p>
<img width="80%" height="602" alt="slide22" src="https://github.com/user-attachments/assets/b5b4d187-1d3d-4450-99a1-9bc15802cb80" />
</p>
<p>
<img width="80%" height="613" alt="slide23" src="https://github.com/user-attachments/assets/31bed54e-ddb8-445e-a613-8e53250bb72c" />
</p>
<p>
After creating the users, I selected one account and attempted to log into Client-1 with it. The login was successful, confirming that the account was active and the domain environment was functioning as intended.
</p>
<p>
<img width="80%" height="626" alt="slide24" src="https://github.com/user-attachments/assets/23f8d68d-2600-4d2b-aba9-a44c8d71e06f" />
</p>
<p>
<img width="80%" height="556" alt="slide25" src="https://github.com/user-attachments/assets/b8253e47-35db-4728-80a4-4463b6b586b3" />
</p>
<p>
<img width="80%" height="643" alt="slide26" src="https://github.com/user-attachments/assets/be03b556-18dd-4c4e-a93c-9aef0f431b85" />
</p>
<p>
This tutorial demonstrated how to deploy and configure a fully functional Active Directory environment using Azure Virtual Machines, simulating both cloud-based and traditional on-prem infrastructure. You built a secure, manageable environment complete with domain services, DNS settings, user provisioning, and group policy configuration.
</p>
<p>
✅ Important: Be sure to clean up your Azure environment after finishing this lab. Close all Remote Desktop sessions, delete any unused Resource Groups, and confirm that all resources have been removed to prevent unnecessary charges.
