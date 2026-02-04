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
<p><br />
<img width="589" height="308" alt="slide6" src="https://github.com/user-attachments/assets/d3cd2d2e-0757-4791-8ff6-5f45805b1165" />
</p>
<p>
From now on you can use Jane_admin as the administrator account. Now we will join Client-1 to the domain (mydomain.com) from the azure portal we will change client-1's DNS settings to the DC's Private IP address. After you do that restart Client-1 from within the Azure portal. Our picture below shows verification that client-1 is on the DC-1 DNS.
</p>
<p>
<img width="1083" height="542" alt="slide7" src="https://github.com/user-attachments/assets/667ffd58-3e47-4de1-a6ff-d4480fe327bc" />
</p>
<p>
<img width="1372" height="722" alt="slide8" src="https://github.com/user-attachments/assets/60eb0001-c67a-4800-a331-06453bf14350" />
</p>
<p>
We have to join Client-1 to the domain in order to do so navigate to your system settings and go to about. Off to the right select rename this pc (advanced). From there select to change the domain. Enter "mydomain.com" after that enter your credentials from mydomain.com\labuser. Your computer will restart and then client-1 will be a part of mydomain.com
</p>
<p>
<img width="1195" height="762" alt="slide9" src="https://github.com/user-attachments/assets/87085299-5c23-4789-b373-0bbeb7470c13" />
</p>
<p>
Wonderufl Client-1 is now a part of the domain. Now we will set up remote desktop for non-administrative users on Client-1. We have to log into Client-1 as an admin and open system properties. Click on "Remote Desktop", allow "domain users" access to remote desktop. After completing those steps you should be able to log into Client-1 as a normal user.
</p>
<p>
<img width="857" height="661" alt="slide10" src="https://github.com/user-attachments/assets/3241e4ba-ca9f-4a9c-b586-657997d8fdb9" />
</p>
<p>
Lastly to verify that normal users can RDP into Client-1 we will use a script to generate thousands of users into the domain. We will input the script in powershell, after the users are created we will select one and RDP into Client-1.
</p>
<p>
<img width="1432" height="978" alt="slide11" src="https://github.com/user-attachments/assets/5b2c7fd2-5a15-4ed1-9cef-fdb0efe3306a" />
</p>
<p>
<img width="672" height="766" alt="slide12" src="https://github.com/user-attachments/assets/6273a363-46a3-4c16-8866-2aa98a9a46c6" />
</p>
<p>
<img width="1134" height="519" alt="slide13" src="https://github.com/user-attachments/assets/e6f249ea-75c1-4c1b-a312-244f63ce0ff7" />
</p>
<p>
As you can see the Powershell script created a user with the username "bab.hubo" We were able to login to Client-1 with his credentials as a normal user.
