<p align="center"
<img src="https://i.imgur.com/09ayVdp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/09ayVdp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/OB0oYlL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a Domain Controller VM (Windows Server 2022) named DC-1, note the Resource Group and Vnetwork that get created at this time. Next, set the Domain Controllers NIC Private IP address to be static. To do this, click on your DC-1 VM -> Networking -> Network Interface -> IP Configurations -> Click on your IP Configuration and set your IP Assignment to "Static".
</p>
<br />
<p>
<img src="https://i.imgur.com/ExKJ6Jm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After Setting DC-1's IP to static, create a Windows 10 VM named "Client-1". Use the same resource group and Vnetwork that was created with DC-1. Ensure that both VMs are in the same Vnetwork. You can verify the topology with Network Watcher. 
</p>
<br />

<p>
<img src="https://i.imgur.com/UZRFZJd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once DC-1 and Client-1 have been created properly, Login to Client-1 with Remote Desktop and ping DC-1's private IP address with ping -t (perpetual ping). 
</p>
<br />
<p>
  <img src="https://i.imgur.com/g4JFqP8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </p>
<br />
<p>
   <img src="https://i.imgur.com/dDfToOR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
   </p>
<br />
<p>
After pinging DC-1, log into DC-1, click start, and type "Windows Defender Firewall with Advanced Security". Click Inbound rules and enable Core Networking Diagnostics - ICMP Echo Request ICMPv4 (Domain and Private). Next do the same for Outbound rules. Check back to Client-1 and verify that the ping succeeded.
</p>
<br />
<p>
  <img src="https://i.imgur.com/3AJNr9J.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </p>
<br />
<p>
  <img src="https://i.imgur.com/Q4p8rjE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </p>
<br />
<p>
After verifying that the ping succeeded, we will install Active Directory. Click start, and enter the Server Manager. Select "Add roles and features" continue with the default settings for Installation type and server selection. At "Server Roles" check the box next to Active Directory Domain Services and click Add Features. Then, select next and install.
</p>
<br />
<p>
<img src="https://i.imgur.com/TMxuQoY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
<p>
Once Installation completes, click on the flag next to "Manage" and select Promote to Domain Controller. Then, the Configuration Wizard will appear. Select Add a new forest and name your domain. I named mine mydomain.com. Next, create your password and continue to the install. The domain controller will then restart. Log back into your domain controller with mydomain.com\labuser as the username. Use the new password you just created.
</p>
<br />
<p>
  
  </p>
<br />
<p>
  
  </p>
<br />
<p>
  <img src="https://i.imgur.com/KN7y0gz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </p>
<br />
<p>
From the Server Manager, select "Tools" and click on Active Directory Users and Computers. Create an Organizational Unit called "_EMPLOYEES" and another named "_ADMINS". Next, in the Employees Organization Unit, create a new user.
</p>
<br />
<p>
<img src="https://i.imgur.com/UiK8e8J.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
<p>
Once the new user has been created, right click on the user and select "Properties". Then, select Member of -> add, and enter "Domain Admins". This adds your user to the Domain Admin Security Group.
</p>
<br />
<p>
<img src="https://i.imgur.com/SPj6NNh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
<p>
Once your user has been created and added to the Domain Admin Security Group, Log off of DC-1 and sign in using your new users account. Your username should look something along the lines of mydomain.com\Jane_admin.
</p>
<br />
<p>
<img src="https://i.imgur.com/aUHyWd6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
<p>
Once you are able to log into DC-1 with your new admin account, we will connect Client-1 to the Domain. Minimize DC-1 and go to the resource group you created in Azure. Select Client-1 -> Networking -> Network Interface -> DNS Servers -> Custom. Then input the private IP address of DC-1 and save. Once saved, restart Client-1 and log in.
</p>
<br />
<p>
<img src="https://i.imgur.com/ZEE94U4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
<p>
Once logged in click system -> Advanced system settings -> Computer Name -> Change -> Domain. Then type in the name of your domain. Mine would be "mydomain.com". Select OK and input your admin credentials. Next, Restart Client-1.
</p>
<br />
<p>
  <img src="https://i.imgur.com/ySXvJDR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </p>
<br />
<p>
  To Verify that Client-1 has joined the domain go to DC-1. Enter Active Directory Users and Computers and select the Computers Organizational Unit. All computers that have joined the domain will be in that folder.
  </p>
<br />
<p>
  <img src="https://i.imgur.com/I3KqQmR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </p>
<br />
<p>
  Next, login to Client-1 with the same credentials used for DC-1. Now that CLient-1 has joined the domain, you can use the same credentials to log into the device.
<br />
<p>
  <img src="https://i.imgur.com/GM64llt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </p>
<br />
<p>
  Next, we will allow for RDP on Client-1 as a normal non-administrator. Once logged into Client-1, click start -> System -> Remote Desktop -> Select users that can remotely access this PC -> Add. Type in "Domain Users", select check names, and click OK. Now, you have enabled RDP for regular domain users.
</p>
<br />
<p>
<img src="https://i.imgur.com/09ayVdp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
<p>
Congrats! Now that that RDP is enabled for regular domain users, you now have installed and configured an Active Directory environment ready to be used!
