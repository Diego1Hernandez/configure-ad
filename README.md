<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


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
- Step 2 Ensure Connectivity between the Client and Domain Controller
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
Create 2 VMs(virtual machines). One bieng the Domain Controller "DC-1" VM(Windows Server 2022), the other being the Client VM "Client -1"(Windows10). Both DC-1 and Clinet1 must be on the same V-net. Next, set DC-1's ping to static in azure.
</p>
<br />

<h2>Step2</h2>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 Use (Remote Desktop) Client 1 to ping DC-1's private IP address using the command prompt ping -t<ip address> (perpetual ping). In DC-1 type "wmf" into the windows search bar and open "Windows Defender Firewall with Advanced Security" --> Inbound Requests -->  ICMPv4 Echo Requests --> enable. Check back at Client-1 to see the ping succeed.
</p>
<br />

<h2>Step3</h2>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
First, login to DC-1 and install Active Directory Domain Services by Server Manager --> add roles/features--> Active Directory domain Services--> Install--> Open. Once open, configure DC-1 and setup a new forest as "mydomain.com"(arbritrary). Lastly, restart and then log back into DC-1 as user: "mydomain.com\labuser".
</p>
<br />

<h2>Step4</h2>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create 2 an Organizational Units(OU) named "_EMPLOYEES" and "_ADMINS" in the Active Directory Users and Computers(ADUC). Now, create a new employee "Jane". Next, add "jane" to the "Domain Admins" Securtiy Group by User-->Properties-->Member of, then type "domain_admins" into the text box--> apply. After, close the Remote Desktop connection to DC-1 and log back in as "mydomain.com\jane".
</p>
<br />

<h2>Step5</h2>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From the Azure Portal, set Client-1's DNS settings to the DC's Private IP address, restart Client-1 from the azure portal. Login to Client-1 using Remote Desktop as the original local admin(labuser) and join it to the domain (causes computer to restart). 
</p>
<br />

<h2>Step6</h2>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login to Client-1 as mydomain.com\jane and allow Domain_users to connect to Client-1 by opening system properties-->Remote Desktop-->Change Users-->domain users--> This allows for normal, non-administrative users to be able to log into Client-1. 
</p>
<br />

<h2>Step7 Verify Success</h2>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login to DC-1 as Jane and open PowerShell_ISE as an administrator. Next, create a new File and paste this script (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) into the file. Run the script and observe the accounts being created. Lastly, attempt to log into Client-1 with one of the accounts (take note of the passowrd in the script). If you are able to log in you have been successful.
