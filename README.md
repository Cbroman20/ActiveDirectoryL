# <h1>Active Directory Homelab</h1>


<h2>Description</h2>
This project will take you through the process of how to set up a basic mock active directory environment from your home desktop. We will run a PowerShell script to generate users, create virtual machines, and install DHCP servers. I recently built my first pc with I5 13th gen processor, 32GB ram, 1TB SSD M.2 storage, and a 24” LG monitor. The main purpose of building my own PC was to learn more about the fundamentals of how computers work and the terminology used when troubleshooting common issues. I hope with my passion for acquiring new knowledge about all things IT that I will grow my knowledge and someday be able to transfer that knowledge to break into the IT field.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Active Directory</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> 

<h2>Program walk-through:</h2>

<h3>Downloads</h3>
First, we download Virtual Box which will host all of our VMs and for that go to [Downloads – Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads) and download your version of the platform package. Once you have done that download the extension pack that supports all platforms. Then download Windows Server 2019 [here](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019) and download windows 10 [here](https://www.microsoft.com/en-us/software-download/windows10) and save them in a place you will remember.

<h3>Creating Virtual Machine </h3>
Open VirtualBox and create a new virtual machine, this is the domain controller, give it an appropriate amount of ram and cores that your physical machine can handle comfortably. Install the windows server 2019 ISO you downloaded on the VM, and add adapter 2 to be an internal network adapter https://imgur.com/a/iXdLB3b. Start the VM and install the Windows Server 2019 Standard Evaluation (Desktop Experience) and custom install.
<p align="center">
Launch the utility: <br/>
<img src="https://imgur.com/a/iXdLB3b" height="80%" width="80%" 
<br />
<br />

<h3>Configure Adapter Ports</h3>
Once in we will configure your adapter ports one is going to be an external adapter connected to your home Wifi the other is going to be an internal port for the network. Rename them to make it easy to differentiate and assign IP address 172.16.0.1 Subnet Mask 255.255.255.0 Gateway empty DNS 127.0.0.1 or loopback address. The external adapter will get its own IP address through DHCP (Dynamic Host Configuration Protocol).

<h3>Install Active Directory Domain</h3>
Open the server manager and we will install the active directory in “add roles and features” and install. Then promote a new domain and name it mydomain.com This will restart the computer you should see MYDOMAIN\Administrator when logging back in. 

<h3>Build Admin Account </h3>
Once logged back in navigate to Active Directory Users and computers and into Mydomain and add a new admin organizational unit. Next, we create an admin account for you. We now have to actually make it an admin account and to do that we add an object name in properties. 

<h3>Install RAS/NAT</h3>
Install remote Access in the server manager and install. After it installs in routing and remote features check NAT then proceed it's likely you will not see the correct screen displaying both your adapters to fix press cancel and repeat the steps. 

<h3>Install DHCP server</h3>
Add the DHCP role and in it, we will set up the scope. Add a new scope to IPv4 and IPv6 and configure to have the internal NIC be the router for the client. 

<h3>Add users through the script in PowerShell</h3>
We will add a script with 1,000 randomly generated users and add you. In this script we have a line creating each user, setting the passwords for each user, hashing user passwords, adding organizational unit for users, and giving usernames. 

<h3>Create windows client </h3>
Create a new VM for the windows client where you will install the windows 10 iso and add an internal network adapter. Then join the domain now you should be able to access the internet, ping the domain controller, log into the computer with any of the users in the domain, and your client should appear on the domain controllers lease list. 

<p align="center">
Launch the utility: <br/>
<img src="https://i.imgur.com/62TgaWL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
