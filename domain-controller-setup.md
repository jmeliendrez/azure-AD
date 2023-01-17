<p align="center">
<img src="https://azure.microsoft.com/svghandler/active-directory/?width=600&height=315" height="50%" width="50%" alt="Azure Logo"/>
</p>

# 🕹 Domain Controller Setup

Setting up a Domain controller consists of installing Active Directory Domain Services onto a Windows Server and then configuring it. This includes the creation of users and groups and assigning security groups to them.

## Video Demonstration

- ### [YouTube: Setting Up Active Directory using Azure](https://youtu.be/i2R2f8Zfrlg)

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

<h2>ACtive Directory Setup</h2>

One of the first steps is to setup 2 Virtual Machines in Azure. The first will be Windows Server 2022 named "DC-1" and the second a Windows 10 machine named "Client-1". If you are unsure on how to do this [click here](https://github.com/jmeliendrez/azure-network-analysis/blob/2cd2fe572ce11bae8a79c1ee91fa427b5fbc9399/setup-vms.md). Once you've set these up your Virtual Machines pane should look like this.

<p>
<img src="https://i.imgur.com/Z3LeeWy.png" height="80%" width="80%" alt=""/>
</p>

Take note of the private IP addresses for both. Then for **DC-1** you will need to make sure that it is asigned a static IP address. This is because it will be the Domain Controller and will need to have an unchanging IP address to allow clients to call back to it for users, group policy, etc. To do this, go to **DC-1** in your virtual machines pane. 

<p>
<img src="https://i.imgur.com/tE80a9s.png" height="80%" width="80%" alt=""/>
</p>

Then on the left hand side click **Networking**. 

<p>
<img src="https://i.imgur.com/RP8zUNl.png" height="80%" width="80%" alt=""/>
</p>

Next, click on the **Network Interface**. 

<p>
<img src="https://i.imgur.com/zYcAw6c.png" height="80%" width="80%" alt=""/>
</p>

Finally, click **IP configurations** on the left-hand side, then **ipconfig-1**. Change **Assignment** from dynamic to static. This will ensure that the DHCP server does not assign the Domain Controller a new IP address when the lease expires (it wont expire now). 

<p>
<img src="https://i.imgur.com/CCbQWba.png" height="80%" width="80%" alt=""/>
</p>

Next, connect to the Server using Remote Desktop.
Once connected, Server Manager will launch automatically. In the top right hand corner click **Manage**. Then, select **Add Roles and Features**.

<p>
<img src="https://i.imgur.com/9I1aU1z.png" height="80%" width="80%" alt=""/>
</p>

A window will open that will guide you through installing Active Directory. Click **Next**.

<p>
<img src="https://i.imgur.com/0wOgaF6.png" height="80%" width="80%" alt=""/>
</p>

In "Select Installation Type" make sure that **Role-based or feature-based installation** is selected. Then, **Next**.

<p>
<img src="https://i.imgur.com/02izKL9.png" height="80%" width="80%" alt=""/>
</p>

On the next screen there is a list of Roles. Select **Active Directory Domain Services**. 

<p>
<img src="https://i.imgur.com/Qi6TD1H.png" height="80%" width="80%" alt=""/>
</p>

When this window appears click **Add Features**.

<p>
<img src="https://i.imgur.com/s9VPNN0.png" height="80%" width="80%" alt=""/>
</p>

Then **Next** and **Install**.

<p>
<img src="https://i.imgur.com/XPf5N7s.png" height="80%" width="80%" alt=""/>
</p>

Installation will run like this. At the end click **Close**.

<p>
<img src="https://i.imgur.com/BeKNXUq.png" height="80%" width="80%" alt=""/>
</p>

Next select the Notification flag on Server Manager. Click **Promote this server to a domain controller**. 

<p>
<img src="https://i.imgur.com/fRla7Mq.png" height="80%" width="80%" alt=""/>
</p>

Another window will open. Here select **Add a new forest**. Then choose a domain name (e.g. billy.com) and click **Next** until you reach **Install**.

<p>
<img src="https://i.imgur.com/xaNlIuC.png" height="80%" width="80%" alt=""/>
</p>

Then, click **Install** This may take a while. Once completed the Server will restart. You will need to login using the domain (billy.com\[user]).


## Creating Users

Now we will create a Domain Admin and a User. To do this we need to go to **Tools**, and **Active Directory Users and Computers**.

<p>
<img src="https://i.imgur.com/UbypMVV.png" height="80%" width="80%" alt=""/>
</p>

Then click on the down arrow next to your domain.

<p>
<img src="https://i.imgur.com/QgIUsQe.png" height="80%" width="80%" alt=""/>
</p>

To create our administrator account, right-click on **Users** then **New**, and **User**.

<p>
<img src="https://i.imgur.com/kBwzojX.png" height="80%" width="80%" alt=""/>
</p>

Fill in the form.

<p>
<img src="https://i.imgur.com/D09NV8b.png" height="80%" width="80%" alt=""/>
</p>

Then go to **Users**, right click *your* new user and select **Properties**.

<p>
<img src="https://i.imgur.com/zhLrtkr.png" height="80%" width="80%" alt=""/>
</p>

Go to **Member Of** at the top of the window.

<p>
<img src="https://i.imgur.com/rjvlk2n.png" height="80%" width="80%" alt=""/>
</p>

Click **Add**. 

<p>
<img src="https://i.imgur.com/xAv4WsI.png" height="80%" width="80%" alt=""/>
</p>

Then type **Domain Admin** and click **Check Names**. The text you typed should now be underlined. Click of **OK**.

<p>
<img src="https://i.imgur.com/0Ihl1Dp.png" height="80%" width="80%" alt=""/>
</p>

Your new user is now part of the Domain Admin group! Now create another User for the domain so that we can login using a Windows 10 machine. 

<p>
<img src="https://i.imgur.com/clpUMzW.png" height="80%" width="80%" alt=""/>
</p>

Once completed you'll need to set up your client PC. [Click here](https://github.com/jmeliendrez/azure-AD/blob/7c15acabf0c963d9802d3fc0ae08995a21e4bf6f/client-setup.md) for that walkthrough.
