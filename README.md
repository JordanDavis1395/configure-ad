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

- Install Active Directory on DC-01
- Promote DC-01 to Domain Controller
- Creating an Administrator in Directory
- Join Client-01 to domain
- Setup Remote Desktop for non-administrative users

<h2>Deployment and Configuration Steps</h2>

1.) Install Active Directory on DC-01.</h3>

- In the Server Manager dashboard, click "Add Roles and Features" and proceed with setup.
<img width="736" alt="AD-setup" src="https://github.com/kirkgacias/ad-deployment-configuration/assets/158519921/bb534e6b-0072-420a-9f74-c03bbcc77016">

<p>

<p><strong> Select Active Directory Domain Services and complete the installation. </strong> </p>


2.) Promote DC-01 to Domain Controller.</h3>

- After the installation is complete, observe the flag in the top left corner the Server Manager.
- Click on the flag and promote DC- to Domain Controller.

<img width="242" alt="notif" src="https://github.com/kirkgacias/ad-deployment-configuration/assets/158519921/3cb91456-cc00-4e70-8ea2-2b54a5dc8137">


-  We will now add a forest and set root domain name to "mydomain.com".
<p>
<img width="565" alt="my domain" src="https://github.com/kirkgacias/ad-deployment-configuration/assets/158519921/e4d06e9a-a5a4-4e8b-b464-b90ac041cbc8"> </p>
  
- Complete the setup restart DC-01.
- Log back in with "your"@mydomain.com.



3.) Creating an Administrator in Directory </h3>

- After DC-01 has reboot, click on Tools and select Active Directory Users and Computers.
- Right on my.com, select New, and then click on Organizational Unit
<img width="438" alt="Users" src="https://github.com/kirkgacias/ad-deployment-configuration/assets/158519921/23db8c79-84f4-4e6d-befe-77505518cb05">


<p><strong> We will be creating OUs named _EMPLOYE and _ADMINS.</strong></p>

<img width="450" alt="admins" src="https://github.com/kirkgacias/ad-deployment-configuration/assets/158519921/d64f8f3b-130b-4156-bc08-b16f7b21fc89">

<p><strong>Right-click on Users and create a new user named Jane Doe with the username jane_admin.</strong></p>

<img width="323" alt="jane doe" src="https://github.com/kirkgacias/ad-deployment-configuration/assets/158519921/5d8f782a-145a-404b-bc83-7a6721b3728d">

<p><strong>Now we will make Jane Doe an administrator by righting her name and adding her to the "Domain Admins" security group.</strong></p>

<img width="412" alt="add to group" src="https://github.com/kirkgacias/ad-deployment-configuration/assets/158519921/08175b12-7a59-4030-b5ef-6ef1983ac6e7">


<p><strong>Logout of DC-01 and log back in with Jane Doe’s credentials</strong></p>

<img width="337" alt="jane login" src="https://github.com/kirkgacias/ad-deployment-configuration/assets/158519921/751f9854-2aa5-4f94-b641-b355e77a2a32">


4.) Join Client-01 to domain </h3>

<p><strong> For Client-01 to join the domain, we first have to set it’s DNS server as DC-01’s private address.</strong></p>

- In the Azure, navigate to Client-01 -> Networking -> Network Interface select DNS Servers.

<img width="735" alt="dns servers" src="https://github.com/kirkgacias/ad-deployment-configuration/assets/158519921/13292c41-67f1-4212-95c4-084ac2ec0751">


<p><strong>Select a custom DNS server, enter private IP address DC-01, and restart Client-01.</strong></p>

<img width="356" alt="dns servers2" src="https://github.com/kirkgacias/ad-deployment-configuration/assets/158519921/d7ec7764-9fcd-4d46-8962-f536bcb1007d">

<p><strong> Now log back in Client- using original admin credentials. Click and go to Settings > this PC (advanced) > Change and add "mydomain.com," then with the created admin credentials (jane_admin).) </strong></p>

<img width="297" alt="remote desktop first login" src="https://github.com/kirkgacias/ad-deployment-configuration/assets/158519921/97df566d-84c9-40d2-88b1-769f79af10a6">

<br>

<p> <strong>Once Client-01 has been added, the VM will restart.</strong></p>


5.) Setup Remote Desktop for non-administrative users </h3>

- Log back into Client- using jane_admin and Settings > Remote Desktop > User Accounts clickSelect users that can access this PC.”
- Add Domain Users.

<br>

<img width="343" alt="domain users" src="https://github.com/kirkgacias/ad-deployment-configuration/assets/158519921/04eaffe2-1fa3-4c4c-a327-8ea5b63e2c24">

<p><strong>This will allow normal users to login to Client-01</strong></p>

<br>

<h2> Concluding Remarks </h2>

<p>
We have successfully completed the Active Directory Deployment and Configuration phase. By configuring Active Directory on the Controller, we established our infrastructure by creating a forest, an administrator account, and Client-01 the domain.</p>
