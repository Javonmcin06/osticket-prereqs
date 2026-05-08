<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 11</b> (21H2)

<h2>List of Prerequisites</h2>

- Create an Azure Virtual Machine WINDOWS 11,4 vCPUS
- Log into VM with Remote Desktop
- IIS Installed
- Windows 11 setup

<h2>Installation Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
PHASE 1: Create Azure Virtual Machine
Go to https://portal.azure.com and create a Virtual Machine running Windows 10 Pro, version 22H2.  Use at least 2 vCPUs and 16 GB of memory. 
Once created, connect to it via Remote Desktop (RDP) using the VM's public IP address.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 Log Into the VM via Remote Desktop
Copy the public IP address of your VM from the Azure portal and connect using Remote Desktop Connection (RDP).
-On Windows: Search Remote Desktop Connection in the Start menu
-Enter the VM's public IP, username labuser, and your password
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
Step 3 — Download the osTicket Installation Files
Inside the VM, download the zip file below and unzip it to the Desktop:
📥 osTicket-Installation-Files.zip
The extracted folder should be named: osTicket-Installation-Files

We will use the files in this folder to install osTicket and all of its dependencies.


Step 4 — Install / Enable IIS with CGI
IIS is required to host osTicket. CGI must be enabled for PHP to function.

Open Control Panel → Programs → Turn Windows Features On or Off
Check ✅ Internet Information Services
Expand: World Wide Web Services → Application Development Features
Check ✅ CGI
Click OK and wait for the install to finish
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

✅ Verify: Open a browser inside the VM and go to 127.0.0.1 — the default IIS page should load.

Step 5 — Install PHP Manager for IIS
From the osTicket-Installation-Files folder, run:
PHPManagerForIIS_V1.5.0.msi
Follow the default installer prompts to complete.
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
Show Image
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
Step 6 — Install the IIS Rewrite Module
From the osTicket-Installation-Files folder, run:
rewrite_amd64_en-US.msi
Follow the default installer prompts to complete.

Show Image
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
Step 7 — Create C:\PHP and Extract PHP 7.3.8

Open File Explorer and create a new folder at: C:\PHP
From the osTicket-Installation-Files folder, extract:

   php-7.3.8-nts-Win32-VC15-x86.zip
→ Extract all contents directly into C:\PHP



Show Image

Step 8 — Install VC Redistributable
From the osTicket-Installation-Files folder, run:
VC_redist.x86.exe
Follow the default installer prompts to complete.

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Show Image

Step 9 — Install MySQL 5.5.62
From the osTicket-Installation-Files folder, run:
mysql-5.5.62-win32.msi
Follow these exact steps in the setup wizard:

Select Typical Setup → Next → Install
✅ Ensure Launch Configuration Wizard is checked → Finish
In the Configuration Wizard, select Standard Configuration → Next
Set the root credentials:

Username: root
Password: root


Click Execute → Finish


<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Show Image

Step 10 — Open IIS as Admin and Register PHP

Search IIS in the Start menu → open as Administrator
In the center panel, double-click PHP Manager
Click "Register new PHP version"
Browse to and select: C:\PHP\php-cgi.exe → OK

Then reload IIS — in the right-side panel, click Stop, then Start.

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Show Image

Step 11 — Install osTicket v1.15.8
From the osTicket-Installation-Files folder:

Unzip osTicket-v1.15.8.zip
Copy the upload folder into: C:\inetpub\wwwroot
Rename the folder: upload → osTicket

Then reload IIS again (Stop and Start the server).

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Show Image

Step 12 — Launch osTicket in the Browser

In IIS, expand the left panel: Sites → Default Web Site → osTicket
On the right panel, click "Browse *:80"

✅ The osTicket installer should now open in your browser!

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Show Image

Step 13 — Enable Required PHP Extensions
Note that some extensions are not yet enabled. Fix this now:

Back in IIS: Sites → Default Web Site → osTicket
Double-click PHP Manager
Click "Enable or Disable an Extension"
Right-click and Enable each of these:

✅ php_imap.dll
✅ php_intl.dll
✅ php_opcache.dll


Refresh the osTicket browser page — the extension checkmarks should update


<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Show Image

Step 14 — Rename ost-sampleconfig.php
In File Explorer, navigate to:
C:\inetpub\wwwroot\osTicket\include\
Rename:

From: ost-sampleconfig.php
To: ost-config.php


<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Show Image

Step 15 — Assign Permissions to ost-config.php

Right-click ost-config.php → Properties → Security → Advanced
Click Disable Inheritance → Remove All
Click Add → Select a Principal
Type Everyone → Check Names → OK
Check Full Control (all boxes) → Apply → OK


<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Show Image

Step 16 — Continue osTicket Setup in the Browser
Click Continue on the osTicket browser setup page and fill in the top section:
FieldValueHelpdesk Name(Your choice)Default Email(Email address that will receive customer tickets)

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Show Image

Step 17 — Install HeidiSQL and Create the Database
From the osTicket-Installation-Files folder, install HeidiSQL.

Open HeidiSQL
Click New (bottom left) to create a new session

Username: root
Password: root


Click Open to connect
In the left panel, right-click the connection → Create New → Database
Name it: osTicket → Click OK


<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Show Image

Step 18 — Complete Installation in the Browser
Back in the browser, fill in the Database Settings section:
FieldValueMySQL DatabaseosTicketMySQL UsernamerootMySQL Passwordroot
Click "Install Now!"

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
Show Image

Step 19 — Installation Complete! 🎉
Congratulations — osTicket is now installed with no errors!
Bookmark these URLs:
PortalURL🔧 Staff / Admin Loginhttp://localhost/osTicket/scp/login.php🌐 End User Portalhttp://localhost/osTicket/

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Show Image
