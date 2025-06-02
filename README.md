<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Deployment and Configuration Steps</h2>

<p>
  
![image](https://github.com/user-attachments/assets/0e91f66e-52e2-4137-b96c-caa3e9c72ed3)


</p>
<p>
The Windows Machine must have a static private IP address. Client-1 will connect to the Windows Machine to verify connectivity by attempting to ping it. Initially, the ping will fail. To resolve this, we need to enable ICMPv4 on the Windows Machine's firewall. Once enabled, Client-1 should be able to ping the Windows Machine successfully. To open the firewall properties click Win+R or use the Windows run command and type "wf.msc"


</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/9614e6e1-cda3-404f-94d0-fa62079708b4)

</p>
<p>
You can check connectivity through Windows Powershell by attempting to ping the private ip address of the virtual machine. As shown above we can see the ping was sent and recieve meaning we do have connection within the network.
</p>
<br />

<p>

![image](https://github.com/user-attachments/assets/ce37b828-23d4-4b49-9b51-dda4dcdc4671)

![image](https://github.com/user-attachments/assets/abc594c2-ab20-42ac-88a1-4d6b2d382cde)
</p>
<p>
When in the deployment configuration choose the option to add a new forest and select the root domain name box, type "mydomain.com" this will be the domain name for your active directory where all the users will be logging into. After this is confirmed we can now go to our Windows Server Manager and install Active Directory. Click the yellow flag in the top right corner and on select server roles chooose "Active Directory Domain Services" then click next till  you reach the confirmation.
</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/74e96c0b-84ec-42f9-b1dc-aaf8629b504e)
</p>
<p>
We can see in the top right of the screen the Active Directory is now getting ready to deploy and install on this Windows Machine, it was shortly after restart to fully download the service.
</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/ad1f5912-dc36-4e72-b00c-f18421a0740f)
</p>
<p>
Restart the virtual machine and log in as mydomain.com\labuser to log onto the Active Directory, it will take a minute or so to load everything up properly.
</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/2e2b06fe-89b3-490d-9e19-0ad3b634f73b)
</p>
<p>
  Now create two Organizational Units (OUs) in the Active Directory Users and Computers console. Right-click on the domain name, select New → Organizational Unit, name the first OU _EMPLOYEES, and click OK. Repeat the process to create a second OU named _ADMINS. Once the _ADMINS OU is created, click on it, right-click inside the OU, and choose New → User. Enter the user details with the first name Jane, last name Doe, and set the username to Jane_admin. Complete the user creation by setting a password and finalizing the setup. After the account is created, right-click on Jane’s user object, select Properties, go to the Member Of tab, and click Add. Type Domain Admins and confirm to add Jane to the Domain Admins security group. Jane Doe is now an admin user with the appropriate privileges.
</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/14f0ac19-f5bc-4e8a-9da6-d533447fbf17)
</p>
<p>
Going forward, you will use the Jane_admin account as the primary administrator. Next, join Client-1 to the domain (mydomain.com). To begin, navigate to the Azure portal and update Client-1’s DNS settings by assigning the Domain Controller's private IP address as its DNS server. Once the DNS settings have been updated, restart Client-1 directly from the Azure portal. After the restart, you can verify that Client-1 is using DC-1 as its DNS server, as shown in the image below.
</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/b5c1a726-49cb-479f-a45e-de00f1a94cf8)
</p>
<p>
Client-1 is now joined to the domain. Next, we'll configure Remote Desktop access for non-administrative users. Log into Client-1 using an administrator account, then open System Properties. Navigate to the Remote Desktop tab and grant Domain Users permission to access Remote Desktop. After completing these steps, standard (non-admin) domain users should be able to remotely log into Client-1.
</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/4c352703-7c5d-4b40-b453-f5eeb2ce8c8a)
</p>
<p>
Creating Active Directory users manually can be time-consuming, especially in large organizations. Using PowerShell, administrators can automate this process with a script that generates random usernames, assigns passwords, and creates the accounts with New-ADUser. The script in PowerShell ISE loops through a set number of users, assigns each to an organizational unit, and enables the account. This saves time, reduces errors, and ensures consistency across user accounts.
</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/dd12e7c4-0a90-4caf-ab2a-ccd38cd8ac05)
</p>
<p>
Here we can see the script generating all the user for the Active Directory.
</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/01eea585-787c-4cce-ba9c-dfb059d3d01c)
</p>
<p>
As you can see the Powershell script created a user with all the usernames and we were able to login to the other virtual machine with any of the created users as an "employee."
</p>
<br />
