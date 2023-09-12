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

<h2>Setup</h2>

- Create a Domain Controller VM (Windows Server 2022) named "DC-1" Take note of the Resource Group and Network (Vnet)
- Set Domain Controller's NIC Private IP address to be static
- Create the Client VM (Windows 10) named "Client-1" with the same Resource Group and Vnet

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
First ensure Connectivity between client and the Domain Controller VM's. Login to Client-1 with Remote Desktop and ping DC-1's private IP address with ping -t. Then login to the Domain Controller and enable ICMPv4 on the loacl windows Firewall. Then check back with Client-1 to see the ping work.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next Install Active Directory. Login to DC-1 and install Active Directory Domain Services. Promote as DC: and setup a new forest as mydomain.com(or whichever name you want) Then restart and log back in to DC-1 as user: mydomain.com\labuser
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next create an Admin and Normal User Account in Active Directory. In Active Directory Users and Computers create an Organizational Unit (OU) called "_EMPLOYEES". Then create another OU named "_ADMINS". Now create a new employee named "Jane Doe" with the username: "jane_admin" and create a password. Then add jane_admin to the "Domain Admins" Security Group. And finally log out or close the Remote Desktop connection to DC-1 and log back in as "mydomain.com\jane_admin"
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next its time to setup Remote Desktop for non-administrative users on CLient-1. Log into Client-1 as mydomain.com\jane_admin and open system properties. Click "Remote Desktop". Then allow "domain users" access to remote desktop.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Finally create a bunch of additional users and attempt to log into client-1 with one of the users. Next login to DC-1 as jane_admin and open PowerShell_ise as an administrator. Create a new file and paste the contents of a script to generate names and create users. Then run the script and observe the accounts being created. When finished attempt to log into Client-1 with one of the accounts and take note of the password in the created script.
</p>
<br />
