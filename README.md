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

<h3>Step 2: Create Virtual Machines</h3>
<p>
Using the same search bar as before, find and select the "Virtual Machines" service. We will now create the Virtual Machine that will host our implementation of osTicket. Start by selecting the "Create" button in the center of the page, then select "Azure virtual machine". Select "Active_Directory" as your Resource Group. We will name our VM "DC-1". Select Windows Server 2022 as the operating system. In order to ensure our VM runs smoothly, we will choose the 2 vcpu, 16 Gib memory size. 
</p>
<img src=https://i.imgur.com/vOJ5nYJ.png/>

























<h2>Deployment and Configuration Steps</h2>
