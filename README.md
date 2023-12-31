<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
Active Directory (AD) is a database and set of services that connect users with network resources. This tutorial is a guide to configuring Active Directory on the Microsoft Azure cloud service.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)

<h3>Step 1: Create the Active Directory Resource Group</h3>
<p>
We will first need to create a Virtual Machine. To do this we will be using a a cloud computing platform called Microsoft Azure: https://portal.azure.com/ . After logging in to your Microsoft Azure account, create a Resource Group. A Resource Group is used to organize and manage Azure resources. You can use resource groups to group related resources for an application. You can find this using the search bar at the top of the page. We will name this Resource Group "Active_Directory". No need to add any tags at this time, select "next" until you are prompted to create the Resource Group.
</p>
<img src=https://i.imgur.com/8NU0JbM.png/>

<h3>Step 2: Create the Domain Controller VM</h3>
<p>
Using the same search bar as before, find and select the "Virtual Machines" service. Start by selecting the "Create" button in the center of the page, then select "Azure virtual machine". Select "Active_Directory" as your Resource Group. We will name our VM "DC-1". Make sure the resource group and all VMs within are set to the same region. Select Windows Server 2022 as the operating system. In order to ensure our VM runs smoothly, we will choose the 2 vcpu, 16 Gib memory size. Set a username and password.
</p>
<img src=https://i.imgur.com/pVYqGTX.png/>

<h3>Step 3: Create the Client VM</h3>
<p>
Repeat the steps for the Domain Controller VM. Resource Group should be set to "Active_Directory". We will name our VM "DC-1". Select Windows 10 Pro as the operating system. Set a username and password. Then click on the "Networking" tab and ensure the virtual network is set to DC-1-vnet.
</p>
<img src=https://i.imgur.com/xCWoQ7e.png/>

<h3>Step 4: Set the Domain Controller to Static IP</h3>
<p>
Within the Virtual Machine page in Azure, select the DC-1 VM. Then select "Networking" -> Network Interface(mine is called dc-1533_z1) -> IP Configurations -> ipconfig1 -> Allocation should be set to Static. Make a note of the static IP for DC-1. Check in the Networking section of both VMs to ensure they are on the same virtual network.
</p>
<img src=https://i.imgur.com/l3FflcD.png/>

<h3>Step 5: Connecting to the VM via Remote Desktop Connection</h3>
<p>
Remote Desktop Connection is a program found on Windows that allows us to remotely access the VM we just created. First find Remote Desktop Connection via the Windows search bar, or type "MSTSC" into the command prompt. Next, enter the Public IP address for the Client-1 VM. This can be found on the "Virtual machines" page to the far right of the screen. You will be asked to enter the credentials you created for the VM.
</p>
<p>
<img src=https://i.imgur.com/vRfL9WX.png/>
</p>

<h3>Step 6: Check connectivity with DC-1</h3>
<p>
Open the command line in the Client-1 VM. Enter the "ping -t" command using the private IP address of DC-1 we recorded in step 4. This will continually check for connectivity. It looks like the connection is timing out. 
</p>
<img src=https://i.imgur.com/RScDj5A.png/>
<p>
We'll have to access DC-1 and adjust some settings. Repeating the same process as we used for Client-1, log into DC-1 with RDP. Find the Windows Firewall by typing "firewall" into the search bar or "mf.msc" into the "Run" app. Select Inbound Rules -> Sort by Protocol -> Enable both copies of "Core Networking Diagnostics - ICMP Echo Request (ICMPv4-In)". The ping command we are using runs on this protocol. If you check back to the Client-1 VM, the ping command should now be receiving responses from DC-1. Ctrl-C will stop the ping command.
</p>
</p>
<img src=https://i.imgur.com/na6hNIf.png/>
<p>

<h3>Step 7: Install Active Directory</h3>
<p>
On DC-1, navigate to Start -> Server Manager -> Add roles and features -> Everything can be left to default -> Server Roles -> Active Directory Services -> Accept installation of any required features -> Select the notification flag icon -> Promote this server to a domain controller -> Add a new forest -> Enter a root domain name, i.e. mydomain.com -> Set a password for Directory Services Restore Mode -> Click "Next" through the windows, install prerequisites -> The VM will restart.
</p>

<h3>Step 8: Re-login to DC-1</h3>
<p>
Double check the public IP and re-login to DC-1. In order to do this we will need to edit the login credentials. Select the small "edit" link on the Remote Desktop Connection Window. -> Use a different account -> enter the domain name you chose / the user name set up for the VM. i.e. mydomain.com/ethan -> use the same password
</p>
<p>
<img src=https://i.imgur.com/5fD9qo4.png/>
</p>

<h3>Step 9: Create User Accounts in Active Directory</h3>
<p>
The Server manager should still be open. Navigate to Tools -> Active Directory Users and Computers -> Right click mydomain.com (Or whatever domain you chose) -> Organizational Unit -> Add an EMPLOYEES and ADMINS Organizational Unit -> Right Click ADMINS -> New -> User -> enter whatever information you prefer for this user
<p>
<img src=https://i.imgur.com/MK7P98s.png/>
</p>
<p>
Within ADMIN right click Jane Doe -> Member Of -> Add -> Enter "domain" and Check Names -> Select Domain Admins -> Apply -> Logoff of DC-1 -> Re-login using mydomoain.com/jane_admin -> Enter the password you set for Jane Doe.
</p>
<p>
<img src=https://i.imgur.com/ytOY086.png/>
</p>

<h3>Step 10: Join Client-1 to your Domain</h3>
<p>
We need to set the DNS server of Client-1 to use DC-1 as the image below illustrates:
</p>
<p>
<img src=https://i.imgur.com/d16xd6x.png/>
</p>
<p>
Return to the Networking window for Client-1 on Azure. Navigate to the Network interface -> DNS Servers -> Custom -> Enter DC-1's private IP -> Save -> Navigate back to the Client-1 VM and select Restart
</p>
<p>
<img src=https://i.imgur.com/oWDbWMH.png/>
</p>
<p>
Log back into Client-1 using RDP -> Right click Start -> System -> Rename this PC (advanced) -> Change... -> Domain -> mydomain.com -> Enter your domain credentials you created for DC-1 -> Restart the VM
</p>
<p>
<img src=https://i.imgur.com/5xuEFD2.png/>
</p>
<p>
We can now use our domain credentials (mydomain.com/jane_admin) to log into Client-1. Next, right click Start -> System -> Remote Desktop -> Select users that can remotely access this PC -> Add -> Enter Domain Users -> Check Names -> OK
</p>
<p>
<img src=https://i.imgur.com/qUmt23t.png/>
</p>
<p>
Ensure everything we have done is working. Return to the DC-1 VM -> Server Manager -> Active Directory Users and Computers -> mydomain.com -> Computers -> Create a new OU called CLIENTS -> Move Client-1 into the CLIENTS OU
</p>
<p>
<img src=https://i.imgur.com/iJSoZUm.png/>
</p>

<h3>Step 11: Create Users</h3>
<p>
  Still logged into DC-1, Using the search bar, Open Powershell ISE as an administrator -> New File
  
Using this [Github Link](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) link, copy and paste the code within the repository into Powershell. -> Go to line 43 of the code. Ensure the Path is set to ou=EMPLOYEES -> Run Script -> This script will create 10,000 random users that we can use to simulate an organization of real people. They will all be located in the EMPLOYEES OU within Active Directory.
</p>
<p>
<img src=https://i.imgur.com/l1DRT7W.png/>
</p>
<p>
After Refreshing the Active Directory Users and Computers, we can select a random user within EMPLOYEES, I chose bafot.leq -> Sign out of Client-1 -> Using the same method as before, use the random user to log into Client-1 -> The password the script created for all the users is Password1
</p>
<p>
<img src=https://i.imgur.com/rsc4QYy.png/>
</p>
<p>
You can observe within C:\Users that a new folder is created each time a new user first accesses the VM. 
</p>
<p>
<img src=https://i.imgur.com/lzuDAUv.png/>
</p>

<h3>Step 12: Test Common User Account Actions</h3>
<p>
If we return to DC-1, we can test a few functions within Active Directory in regards to users. If, for example, a user attempts too many logins and their account locks, you can navigate to the EMPLOYEE OU -> bafor.leq(Whichever user is experiencing the issue) -> Account -> Check the Unlock Account box -> Apply. You can also reset user passwords, enable or disable their account, or move them to a new Organizational Unit. These functions would all be useful in a variety or organizations
</p>
<p>
<img src=https://i.imgur.com/0V375YL.png/>
</p>

<h4>We have now successfully set up Active Directory on our Domain Controller and Client. I hope this tutorial was helpful, if you have any questions or suggestions on how I can improve this guide, please feel free to contact me at: efblomquist@gmail.com</h4>
