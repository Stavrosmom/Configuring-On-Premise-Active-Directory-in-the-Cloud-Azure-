<p align="center"
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

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a Domain Controller VM (Windows Server 2022) named DC-1, note the Resource Group and Vnet that get created at this time. Next, set the Domain Controllers NIC Private IP address to be static. To do this, click on your DC-1 VM -> Networking -> Network Interface -> IP Configurations -> Click on your IP Configuration and set your IP Assignment to "Static".
</p>
<br />
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After Setting DC-1's IP to static, create a Windows 10 VM named "Client-1". Use the same resource group and vnet that was created with DC-1. Ensure that both VMs are in the same Vnet. You can verify the topology with Network Watcher. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once DC-1 and Client-1 have been created and configured properly, Login to Client-1 with Remote Desktop and ping DC-1's private IP address with ping -t (perpetual ping) 
</p>
<br />
After pinging DC-1, log into DC-1, click start, and type "Windows Defender Firewall with Advanced Security". Click Inbound rules and enable Core Networking Diagnostics - ICMP Echo Request ICMPv4 (Domain and Private). Next do the same for Outbound rules. Check back to CLient-1 and verify that the ping succeeded.
</p>
<br />
<p>

</p>
<br />
<p>

</p>
<br />
<p>

</p>
<br />
<p>

</p>
<br />
<p>

</p>
<br />
<p>

</p>
<br />
<p>

</p>
<br />
<p>

</p>
<br />
<p>







