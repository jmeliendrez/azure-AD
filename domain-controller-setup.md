<p align="center">
<img src="https://azure.microsoft.com/svghandler/active-directory/?width=600&height=315" height="50%" width="50%" alt="Azure Logo"/>
</p>

# 🕹 Domain Controller Setup

Setting up a Domain controller consists of installing Active Directory Domain Services onto a Windows Server and then configuring it. This includes the creation of users and groups and assigning security groups to them.

## Video Demonstration

- ### [YouTube: Setting Up Active Directory using Azure]()

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines)
- Microsoft Remote Desktop

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10

<h2>List of Prerequisites</h2>

- Microsoft Azure Subscription
- Reliable Internet Connection
- Microsoft Remote Desktop

<h2>Project Setup</h2>

One of the first steps is to setup 2 Virtual Machines in Azure. The first will be Windows Server 2022 named "DC-1" and the second a Windows 10 machine named "Client-1". If you are unsure on how to do this [click here](https://github.com/jmeliendrez/azure-network-analysis/blob/2cd2fe572ce11bae8a79c1ee91fa427b5fbc9399/setup-vms.md). Once you've set these up your Virtual Machines pane should look like this.

<p>
<img src="" height="80%" width="80%" alt=""/>
</p>

Take note of the private IP addresses for both. Then for **DC-1** you will need to make sure that it is asigned a static IP address. This is because it will be the Domain Controller and will need to have an unchanging IP address to allow clients to call back to it for users, group policy, etc. To do this, go to **DC-1** in your virtual machines pane. 

<p>
<img src="" height="80%" width="80%" alt=""/>
</p>

Then on the left hand side click **Networking**. 

<p>
<img src="" height="80%" width="80%" alt=""/>
</p>

Next, click on the **Network Interface**. 

<p>
<img src="" height="80%" width="80%" alt=""/>
</p>

Finally, click **IP configurations** on the left-hand side, then **ipconfig-1**. Change **Assignment** from dynamic to static. This will ensure that the DHCP server does not assign the Domain Controller a new IP address when the lease expires (it wont expire now). 

<p>
<img src="" height="80%" width="80%" alt=""/>
</p>

Next, connect to the Server using Remote Desktop.

<p>
<img src="" height="80%" width="80%" alt=""/>
</p>

Once connected, 
