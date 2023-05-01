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
<img src="https://i.imgur.com/oH3HGIg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once we install osTicket, we will have an osTicket zip folder in the downloads. We will click on this folder and see that there is an "upload" folder. We will drag this "upload" folder into C:\inetpub\wwwroot. Then we will rename the "upload" folder to "osTicket". 
</p>
<br />

<p>
<img src="https://i.imgur.com/cr7GiAU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We will go back to IIS, click on the server, and restart again. We then will go to Sites->Defualt Web Site->osTicket and then click on Browse *:80 (http) on the right side of the directory. This will allow us to successfully access osTicket in the browser, but we will need to enable some features for improvements.
</p>
<br />

<p>
<img src="https://i.imgur.com/tdQvN9E.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To enable these feautres, we will go back to IIS and go to [our server]->Sites->Default Web Site->osTicket->PHP Manager->Enable or Disable and extension. We will enable: php_imap.dll, php_intl.dll, php_opcache.dll

</p>
<br />

<p>
<img src="https://i.imgur.com/gp4Ra40.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We are going to locate C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php and rename it to C:\inetpub\wwwroot\osTicket\include\ost-config.php. We then will assign permissions to this file, First we will disable inheritence by right clicking on the file->properties->security->advanced->disable inheritance->remove all inherited permissions from this object. Then we will add permissions by going to select principle and type "everyone" under "Enter the object name to select". Check names, and then check the box that says "Full Control" click on "apply" and then "ok".

</p>
<br />

<p>
<img src="https://i.imgur.com/3rDmgsH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We will continue to setting up osTicket by putting in the information that we are being asked. Before clicking "install now" we will go to HeidiSQL and create a new database called "osTicket". We will type the name of this database where it says "mySQL Database" on the browser.  We have successfully accessed osTicket, now we will delete C:\inetpub\wwwroot\osTicket\setup and then we will set permissions to "read" only on C:\inetpub\wwwroot\osTicket\include\ost-config.php.

</p>
<br />
