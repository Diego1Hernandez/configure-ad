<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1 Set up Resources in Azure
- Step 2 Ensure Connectivity between teh client and Domain Controller
- Step 3 Install Active Directory
- Step 4 Create an Admin and Normal User Account in AD
- Step 5 Join Client-1 to your domian
- Step 6 Setup Remote Desktop for non-administrative users on Client-1
- Step 7 Create users and attempt to log into client-1 with one of the users (verifying your work)

<h2>Deployment and Configuration Steps</h2>

<h2>Step1</h2>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
First, create the domain controller VM(Windows Server 2022) named "DC-1". Next, set the DC-1's NIC Private IP address to static. Now, Create the Client VM(Windows10) named "Client-1". Make sure to use the same resource group and Vnet that you created in the step before this one. Now, Ensure that both VMs are in teh same Vnet(this can be done by checking the topology with Network Watcher. 
</p>
<br />

<h2>Step2</h2>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
First, login to Client-1 with Remote Desktop and ping DC-1's private IP address using the command prompt ping -t<ip address> (perpetual ping). Next, login to the DC-1 and enable ICMPv4 in the local windows firewall. Lastly, check back at Client-1 to see the ping succeed.
</p>
<br />

<h2>Step3</h2>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
First, login to DC-1 and install Active Directory Domain Services. Next, promote as a DC: Setup a new forest as "mydomain.com"(arbritrary). Lastly, restart and then log back into DC-1 as user: "mydomain.com\labuser.
</p>
<br />

<h2>Step4</h2>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
