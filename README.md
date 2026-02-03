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
<h2>Installation Steps</h2>
Welcome to my first in-depth IT tutorial! To begin we will have to create a Virtual machine using the Microsoft Azure portal(portal.azure.com). We will be using a VM(virtual machine) which is a remote computer. We are using a VM in order to protect our physical machine just in case something malfunctions, and also have a clean slate computer to continually replicate the lab on. Create a resource group and title it "osTicket". Afterwards create a VM with 2-4 CPUs. In this example I will be using 4 CPUs.
<p>
<p>
<img width="864" height="422" alt="slide1modify1" src="https://github.com/user-attachments/assets/4f9d1226-2ab2-464d-8b82-060411a8e9bf" />

</p>
<p>
