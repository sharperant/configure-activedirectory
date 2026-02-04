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

<h2>Deployment and Configuration Steps</h2>
</p>
<p>
In this lab we will create two VMs in the same VNET. One will be a Domain Controller, the other will be a Client machine. We will change the DC to a static IP because its offering Active Directory services to the client machine. Client machine will be joined to the domain. We will control the DNS settings on the client machine, the client machine will use the DC as its DNS server.
</p>
<p>
<img width="1004" height="858" alt="slide1" src="https://github.com/user-attachments/assets/38958b04-816b-4ada-9e9d-cddfff56c248" />
</p>
<p>
DC-1 has to have a static Private IP Address. Client one will connect to DC-1 to ensure connectivity we will try to ping DC-1 from Client-1. At first the ping will not work correctly. We have to enable ICMPv4 on the firewall on DC-1. Now we can ping DC-1 successfully from Client-1.
</p>
<p>
<img width="1015" height="767" alt="slide2" src="https://github.com/user-attachments/assets/1cb96d1d-2f5d-4902-a1b3-dd009f99d2cc" />
</p>
<p>
<img width="977" height="510" alt="slide3" src="https://github.com/user-attachments/assets/791d09fb-376f-4eba-b1c9-ffca477f7b9c" />
</p>
<p>
Now we will log back into DC-1 to install AD Users & Computers. Promote the VM to DC, setup a new forest as "mydomain.com" afterwards restart then log back into DC-1 as user: "mydomain.com\labuser". If you performed the steps properly you should be able to run AD Users & Computers as shown below.
</p>
<p>
<img width="752" height="528" alt="slide4" src="https://github.com/user-attachments/assets/5e5d5a3b-dc25-458e-858d-c88bdec0e6c5" />
</p>
<p>
Excellent! We can start creating Organizational Units (OU). Let's first create an OU named _EMPLOYEES. Create another OU named _ADMINS. In order to do that right click on the domain area. Select new->Organizational Unit and fill out the field. Then click inside of your OU and right click, select new and select user and fill out the information for your new user. The user should be named Jane Doe, she is going to be an Admin so her username will be Jane_admin. Lastly add Jane to the domain admins security group.
</p>
<p>
<img width="1358" height="484" alt="slide5" src="https://github.com/user-attachments/assets/5568744e-30bf-4992-84ca-0c23a5c7a740" />
</p>
<p>
<img width="589" height="308" alt="slide6" src="https://github.com/user-attachments/assets/d3cd2d2e-0757-4791-8ff6-5f45805b1165" />
</p>
<p>
From now on you can use Jane_admin as the administrator account. Now we will join Client-1 to the domain (mydomain.com) from the azure portal we will change client-1's DNS settings to the DC's Private IP address. After you do that restart Client-1 from within the Azure portal. Our picture below shows verification that client-1 is on the DC-1 DNS.
</p>
<p>
