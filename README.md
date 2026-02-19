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
<img width="1036" height="560" alt="slide1" src="https://github.com/user-attachments/assets/17fc0484-96a7-4ef7-8077-2c4d5f24b8fd" />
</p>
<p>
<img width="1037" height="560" alt="slide2" src="https://github.com/user-attachments/assets/6a7da878-8bde-48c6-b9b2-9b588c928e47" />
</p>
<p>
I also deployed a Windows 10 VM named "Client-1" in the same VNet, region, and resource group as the domain controller to ensure proper communication between the two machines.
</p>
<p>
<img width="1035" height="561" alt="slide3" src="https://github.com/user-attachments/assets/eada7311-f98a-460b-98d1-53365500ee45" />
</p>
<p>
Set Domain Controller’s NIC Private IP address to be static:
</p>
<p>
<img width="1035" height="565" alt="slide4" src="https://github.com/user-attachments/assets/1a7e7e31-8c0a-4463-be0d-a8967819a739" />
</p>
<p>
<img width="1035" height="563" alt="slide5" src="https://github.com/user-attachments/assets/9f8eb5c0-7644-4f0d-9a1b-1d99d558c33c" />
</p>
<p>
Ensure Connectivity between the client and Domain Controller. To verify network connectivity, I logged into Client-1 using Remote Desktop and continuously pinged DC-1’s private IP using the ping -t command.
</p>
<p>
<img width="1035" height="437" alt="slide6" src="https://github.com/user-attachments/assets/86aa9e2d-0a41-41de-be60-c4c1c62a2085" />
</p>
<p>
I then logged into DC-1 and enabled ICMPv4 (ping) through the local Windows Firewall.
</p>
<p>
<img width="1040" height="562" alt="slide7" src="https://github.com/user-attachments/assets/ac063d96-31ec-4324-a77a-a92249b59022" />
</p>
<p>
I confirmed back on Client-1 that the ping was successful, indicating proper connectivity.
</p>
<p>
<img width="1042" height="445" alt="slide8" src="https://github.com/user-attachments/assets/d769ca3d-7aa6-4256-bb47-2e9309475c35" />
</p>
<p>
Installing Active Directory. Next, I installed Active Directory Domain Services on DC-1 and promoted it to a Domain Controller by creating a new forest called mydomain.com (or myadproject.com).
</p>
<p>
<img width="1038" height="616" alt="slide9" src="https://github.com/user-attachments/assets/c1f20043-806e-4361-a6b6-28cc2f7ecef4" />
</p>
<p>
Promoting it as a Domain Controller
</p>
<p>
<img width="1037" height="620" alt="slide10" src="https://github.com/user-attachments/assets/6a6231bd-5def-48dc-904a-df4ae0f98f97" />
</p>
<p>
<img width="1038" height="618" alt="slide11" src="https://github.com/user-attachments/assets/72a2c733-0a68-466d-9bfd-f58cbe7ef582" />
</p>
<p>
After the system rebooted, I logged into DC-1 using the domain account mydomain.com\labuser.
</p>
<p>
<img width="1030" height="538" alt="slide12" src="https://github.com/user-attachments/assets/83475086-c312-4c97-9429-58a7f6f83f5e" />
</p>
<p>
