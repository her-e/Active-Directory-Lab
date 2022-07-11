<h1>Active Directory lab - Configuring Domain Controller and Networks</h1>

<h2>Description</h2>
In this lab, I am going to walk through how to create an Active Directory home lab Environment using Oracle VirtualBox. Configuring and running this lab will definitely help develop our understanding of how active directory and windows networking works. In this lab, we will be creating our domain controller on a virtual machine that has two network adapters. This will connect to our outside internet and the other network adapter will connect to our VirtualBox private network. This will allow our client's PC to connect to the internet through the domain controller. We will also be configuring our NAT and routing, DHCP, DNS, IP Address on the domain controller, and Client PC on another virtual machine. This will allow us to apply Group Policy Objects and provision, maintain, and deprovision users in Active Directory.
 <br/>
 <br/>
 <b>Lab Requirements:</b>
  <ul>
    <li>  Windows Server 2019 ISO </li>
    <li>  Windows 10 ISO </li>
    <li>  Oracle VirtualBox Installation </li>    
  </ul>
<br/>
There will be 3 parts to complete this Lab:
<br/>
<br/>
1. Set up and configure <B>Domain Controller</B>.
<br/>
  <ul>
    <li> Assign <B>IP Address</B> to Internal Network </li>
    <li> Rename Server to "DC" (Domain Controller) </li>
    <li> Add Active Directory Domain Services </li>
    <li> Promote Domain Controller </li>
    <li> Create Domain Admin Account </li>   
  </ul>
<br/>
2. Configure Networks.
  <ul>
    <li> Remote Access Server <B>(RAS)</B> and Network Address Translation <B> (NAT)</B> </li>
    <li> Dynamic Host Configuration Protocol Server<B> (DHCP)</B> </li>
  </ul>
<br/>
3. Create new Windows 10 Virtual Machine and join Domain.
<br />
 <h2> Languages and Utilities Used </h2>
  <ul>
    <li> <b>Oracle VirtualBox</b> </li>
  </ul>
<h2>Environments Used </h2>
  <ul>
    <li> <b>Windows Server 2019</b> </li>
    <li> <b>Windows 10</b> (21H2) </li>
  </ul>



<h2>Program walk-through:</h2>

<h3>Part 1: Set up and Configure Domain Controller:<h3>

<p align="center">
Install Windows Server 2019:
<br/>
Note: Enabled 2 network adapter before starting up (NAT and Internal Network)
<br/>
<img src="https://imgur.com/Ql6Dp97.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />
Assign IP Address (172.16.0.1), Subnet Mask (255.255.255.0), and Preferred DNS (127.0.0.1) to Internal Network:  <br/>
<img src="https://imgur.com/ADSxZOl.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />
Rename PC to "DC" (Domain Controller), then restart:  <br/>
<img src="https://imgur.com/bCO6g4l.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />
Add Features and Roles: Active Directory Domain Services:  <br/>
<img src="https://imgur.com/xl1leju.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />
Promote Domain Controller (Herlabs.com):  <br/>
<img src="https://imgur.com/JV3nZHa.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />
Create User in New Organizational Unit (ADMINS_):  <br/>
<img src="https://imgur.com/HGjXS9Y.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />
Promote User to Domain Admin Account (Member of Domain Admins), then sign into New Domain Admin Account:  <br/>
<img src="https://imgur.com/bZht3Tk.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />

<h3>Part 2: Configure Networks (RAS/NAT ,DHCP):<h3>
<p align="center">
Install and Configure Remote Access Service (Add Roles and Feature):
<br/>
Add Feature "Remote Access" in Server Roles, then add Feature "Routing" and "DirectAccess and VPN (RAS)" in Roles Services, then Install: <br>
<img src="https://imgur.com/bZht3Tk.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />
Configure and Enable Routing and Remote Access, Select "NAT", then Select Internet (DON'T Select Internal Network), Finish Configuration: <br>
<img src="https://imgur.com/dpwGi5s.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />
Install DHCP Server in Add Roles and Feature, then Configure (Create New Scope in IPv4):<br/>
Scope Name: 172.16.0.100-200<br>
<img src="https://imgur.com/TnNySjD.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />
Configure Start (172.16.0.100) and End (172.16.0.200) IP Address, and Subnet Mask (255.255.255.0):<br/>
<img src="https://imgur.com/RhyBLK9.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />
Set Lease Duration (3 days for this Lab):<br/>
<img src="https://imgur.com/liBFyqF.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />
Add IP Address to Router (Default Gateway):<br/>
<img src="https://imgur.com/LzREENM.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />
Activate Scope and Authorize:<br/>
<img src="https://imgur.com/G7zu3DE.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />


<h3>Part 3: Create new Windows 10 Virtual Machine and join Domain.:<h3>
<p align="center">
Set up Windows 10 (New VM), Verify IP Address for 172.16.0.100 on Command Prompt, then Ping www.google.com to verify network connection.
<br/>
Note: Network Adapter set to Internal Network
<img src="https://imgur.com/D5NEYXr.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />
Rename PC to "Client1" and join Domain (Herlabs.com).
<img src="https://imgur.com/B2FtoKf.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />

<img src="https://imgur.com/PtFB6V8.png" height="80%" width="80%" alt="Active Directory"/>
<br />
<br />

<h2>Results</h2>
<h3>Look up Address Lease to Client1 on Domain Controller (Herlabs.com)</h3>
<p align="center">
<img src="https://imgur.com/STMkoaG.png" height="80%" width="80%" alt="Active Directory"/>


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
