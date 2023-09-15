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
<img src="https://i.imgur.com/VhCkqTY.png" height=70% width=70%/>
</p>
<p>
First, ensure Connectivity between the client and the Domain Controller VMs. Log in to Client-1 with Remote Desktop and ping -t. Notice that it will not connect.
</p>
<br />

<p>  
<img src="https://i.imgur.com/kl8EAx2.png" height=80% width=80%/>
</p>
<p>  
<img src="https://i.imgur.com/SEGuSm4.png" height=80% width=80%/>
</p>
<p>
Then login to the Domain Controller and enable ICMPv4 on the local Windows Firewall. Check back with Client-1 to see the ping work.
</p>
<br />

<p>
<img src="https://i.imgur.com/aM5eZsM.png" height=70% width=70%/>
</p>
<p>
<img src="https://i.imgur.com/lUOJKFy.png" height=70% width=70%/>
</p>
<p>
Next, Install Active Directory. Login to DC-1 and install Active Directory Domain Services. Promote as DC: and set a new forest as mydomain.com(or whichever name you want) Then restart and log back into DC-1 as user: my domain.com\labuser
</p>
<br />

<p>
<img src="https://i.imgur.com/dF5zje2.png" height=70% width=70%/>  
</p>
<p>
<img src="https://i.imgur.com/JrbxqCx.png" height=50% width=50%/>  
</p>
<p>
<img src="https://i.imgur.com/lgvAWkw.png" height=50% width=50%/>
</p>
<p>
Next, create an Admin and Normal User Account in the Active Directory. In Active Directory Users and Computers create an Organizational Unit (OU) called "_EMPLOYEES". Then create another OU named "_ADMINS". Now create a new employee named "Jane Doe" with the username: "jane_admin" and create a password. Then add jane_admin to the "Domain Admins" Security Group. Finally, log out or close the Remote Desktop connection to DC-1 and log back in as "my domain.com\jane_admin"
</p>
<br />

<p>
<img src="https://i.imgur.com/AvvvJr1.png" height=70% width=70%/>
</p>
<p> 
Make sure to set the Client-1 VM's DNS to the Private IP Address so that it can connect to the domain controller.
</p>
<br />

<p>
<img src="https://i.imgur.com/GpjrWQZ.png" height=70% width=70%/>
</p>
<p>
<img src="https://i.imgur.com/i2sTLeX.png" height=50% width=50%/>
</p>
<p>
Connect Client-1 to the Domain Controller so that it can appear in the Active Directory in the Computers folder. 
</p>
<br />

<p>
<img src="https://i.imgur.com/uLn0dCE.png" height=50% width=50%/>
</p>
<p>
<img src="https://i.imgur.com/3TR6Tjd.png" height=50% width=50%/>
</p>
<p>
Next, it's time to set up a Remote Desktop for non-administrative users on CLient-1. Log into Client-1 as mydomain.com\jane_admin and open system properties. Click "Remote Desktop". Then allow "domain users" access to remote desktop.
</p>
<br />

<p>
<img src="https://i.imgur.com/yUUgKQK.png" height=70% width=70%/>
</p>
<p>
<img src="https://i.imgur.com/3saTZCd.png" height=70% width=70%/>
</p>
<p>
Finally, create a bunch of additional users and attempt to log into client-1 with one of them. Login to DC-1 as "jane_admin" and open "PowerShell_ise" as an administrator. Create a new file and paste the contents of a script to generate names and create users(this was created for this lab). Then run the script and observe the accounts being created. When finished attempt to log into Client-1 with one of the accounts and take note of the password in the created script.
</p>
<br />
