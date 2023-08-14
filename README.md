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
Repeat the steps for the Domain Controller VM. Resource Group shpuld be set to "Active_Directory". We will name our VM "DC-1". Select Windows 10 Pro as the operating system. Set a username and password. Then click on the "Networking" tab and ensure the virtual network is set to DC-1-vnet.
</p>
<img src=https://i.imgur.com/xCWoQ7e.png/>

<h3>Step 4: </h3>
<p>
Within the Virtual Machine page in Azure, select the DC-1 VM. Then select "Networking" -> Network Interface(mine is called dc-1533_z1) -> IP Configurations -> ipconfig1 -> Allocation should be set to Static. Make a note of the static IP for DC-1.
</p>
<img src=/>

<h3>Step 5: </h3>
<p>

</p>
<img src=/>




















<h2>Deployment and Configuration Steps</h2>
