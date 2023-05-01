<p align="center">
<img src="https://i.imgur.com/TpTvrlK.png" alt="osTicket logo"/>
</p>

<h1>Setup Resources in Azure & Ensure connectivity between client and Domain Controller</h1>
This tutorial outlines the setup process of virtual machines created in Azure and checking the connectivity between the client and Domain Controller.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Command Prompt

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)


<h2>Virtual Machines Creation Steps</h2>

For this project, I created two virtual machines. One will be the client, and the other one will be the domain controller.

<p>
<img src="https://i.imgur.com/j0QOhKa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Our domain controller(DC-1) will have a Windows Server OS. After creating a username and password, we can click on "create" and the virtual machine will automatically create a virtual network. 

</p>
<br />
<p>
<img src="https://i.imgur.com/KygT9cP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/jcBLuiu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Our Client-1 machine will have a Windows 10 OS, and we will put it in the same virtual network that our DC-1 is in.
</p>
<br />

<p>
<img src="https://i.imgur.com/B5skk2O.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We will then set DC-1's NIC's private IP address to be static. We can do this by going to our DC-1 virtual machine in Azure->Networking->Click on the Network Interface->IP Configurations->Click on the line where it has the Private IP address(dynamic)->switch assignment from "dynamic" to "static".
</p>
<br />

<p>
<img src="https://i.imgur.com/QKGv7oZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we will remote connect to both DC-1 and Client-1 virtual machines. We are going to ensure connectivity between the two machines using the "ping" command in the command line. We will get DC-1's private IP address from Azure, and type "ping -t [DC-1's private IP address] on Client-1's command line. We should get a perpetual response "requeset timed out". We will go to DC-1's machine and enable ICMPv4 on the local Widnows firewall. We can do this by going to Windows Defender Firewall with Advanced Security->Inbound Rules->*Enable* both rules that are named "Core Networking Diagnostics - ICMP Echo Request (ICMPv4-in)". We will go back to Client-1's machine to check the connectivity in the command line, and it should look like the image above.
</p>
<br />
