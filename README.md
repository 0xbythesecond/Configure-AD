<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
Active Directory centrally manages thousands of user accounts in a single place (accounts, passwords and permissions) as well as manage devices on a large scale.
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

- Domain Controller VM (Windows Server 2022) named “DC-1”
- Domain Controller’s NIC Private IP address to be static
- ICMPv4 (ping) was allowed on the Domain Controller
- Step 4

<h2>Deployment and Configuration Steps</h2>
<p>
Firstly, we will need to establish the resource group so that you can add your virtual machines for the Domain Controller (DC-1) and the Client Virtual Machine (Client-1). The Domain Controller VM will use Windows Server 2022 system image (a serialized copy of the entire state of a computer system stored in some non-volatile form such as a file). The Domain Controller’s NIC Private IP address is set to static. The Client VM (Windows 10) named “Client-1” was created with the same Resource Group and Vnet that was created in DC-1. 
</p>
<p align="center">
<img src="https://i.imgur.com/lKmRcIy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p> IP address set to static (static IP addresses are necessary for devices that need constant access.)</p>
<p align="center">
<img src="https://i.imgur.com/n3KceWF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
<p>
Second, check for connection between the client device and domain controller by logging into Client-1 with Remote Desktop Connection (RDP) and pinging DC-1’s private IP address using ping -t (perpetual ping). ICMPv4 (ping) was allowed on the Domain Controller's (DC-1) Firewall in Windows Firewall (Core Networking Diagnostics - ICMP Echo Request (ICMPv4-In)). After logging back into Client-1 check to make sure the ping is successful.
</p>
<p align="center">
<img src="https://i.imgur.com/FWLTP8X.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p> Pictured below displays that the icmp rule has been allowed on the windows firewall for inbound traffic: </p>
<p align="center">
<img src="https://i.imgur.com/f4i0pdh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>  
<br />
<p>
While in DC-1, we've selected to 'add roles and features' to enable Active Directory Domain Services. Promoted as a DC: a new forest as mydomain.com setup. Remote Desktop was Restarted and logged back into DC-1 as user: mydomain.com\labuser.
</p>
<p align="center">
<img src="https://i.imgur.com/ipCHp9t.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p></p>
<p align="center">
  <img src="https://i.imgur.com/Ccbt7ak.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
<p> Next, we configure the organizational units for the admins and employees in Active Directory (AD) while continuing to be in DC-1 (Remote Desktop Connection).  The accounts can now be viewed in Active Directory in the appropriate organizational unit. In the Active Directory, right click on your <b>domain name</b> and move your mouse to hover <b>new</b>--><b>Organizational Unit</b> and left click to create folders for your AD. We will create employees, admins, and security groups.
</p>
<p align="center">
<img src="https://i.imgur.com/D59IbY9.png" height="80%" width="80%" alt="Active Directory OU"/>
  </p>
</br>
<p> Create a new OU named '_ADMINS' --> Create a new employee named <b>Karen What</b> (same password) with the username of <b>'karen_admin'</b>. Once the admin is created, add "karen_admin" to the "domain admins" security group.</p>
<p align="center">
<img src="https://i.imgur.com/Qzlpsyk.png" height="80%" width="80%" alt="Add user to domain admins"/>
  </p>
  </br>
<p>Log out and close the connection to dc-1 for current user(mydomain.com\labuser) and log back in as "mydomain.com\karen_admin".<p/>
<p align="center">
<img=src"https://i.imgur.com/WiQI5sG.png" height="80%" width="80%" alt="cmd displays new logged in user"/>
 </p>
  </br>
  <p>
  PowerShell_ise was opened as an administrator. A new File was created and pasted into the contents of the script. When the script is run, account will created.</p>

