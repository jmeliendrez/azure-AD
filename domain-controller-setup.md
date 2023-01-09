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

Once connected, Server Manager will launch automatically. In the top right hand corner click **Manage**.

<p>
<img src="" height="80%" width="80%" alt=""/>
</p>

Then, select **Add Roles and Features**.

A window will open that will guide you through installing Active Directory. Click **Next**.

In "Select Installation Type" make sure that **Role-based or feature-based installation** is selected. Then, **Next**.

On the next screen there is a list of Roles. Select **Active Directory Domain Services**. 

When this window appears click **Add Features**.

Then **Next** and **Install**.

Installation will run like this. At the end click **Close**.

Next select the Notification flag on Server Manager. Click **Promote this server to a domain controller**. 

Another window will open. Here select **Add a new forest**. Then choose a domain name (e.g. billy.com) and click **Next** until you reach **Install**.

Then, click **Install** This may take a while. Once completed the Server will restart. You will need to login using the domain (billy.com\[user]).

## Creating Users

Now we will create a Domain Admin and a User. To do this we need to go to **Tools**, and **Active Directory Users and Computers**.

Then click on the down arrow next to your domain.

To create our administrator account, right-click on **Users** then **New**, and **User**.

Fill in the form.

Then go to **Users**, right click your new user and select **Properties**.

Go to **Member Of** at the top of the window.

Click **Add**. Then type **Domain Admin** and click **Check Names**. The text you typed should now be underlined. Click of **Ok**.

Your new user is now part of the Domain Admin group! Now create another User for the domain so that we can login using a Windows 10 machine. Once completed you'll need to set up your client PC. [Click here](https://github.com/jmeliendrez/azure-AD/blob/7c15acabf0c963d9802d3fc0ae08995a21e4bf6f/client-setup.md) for that walkthrough.


