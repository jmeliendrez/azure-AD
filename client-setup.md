<p align="center">
<img src="https://azure.microsoft.com/svghandler/active-directory/?width=600&height=315" height="50%" width="50%" alt="Azure Logo"/>
</p>

# 🖥 Client Setup

Setting up a client for a server is a vital task in any organisation. Below, I walkthrough the various steps that go into connecting a client to the Domain Controller. If you haven't already, I recommend going through the [Domain Controller](https://github.com/jmeliendrez/azure-AD/blob/b4b35cc0f775e8c192a90408640e78e80684d0a6/domain-controller-setup.md) setup first.

## Video Demonstration

- ### [YouTube: Connecting a Client to a Domain Controller]()

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines/Compute)
- Microsoft Remote Desktop

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10

<h2>List of Prerequisites</h2>

- Microsoft Azure Subscription
- Reliable Internet Connection
- Microsoft Remote Desktop

<h2>Client Setup</h2>

After setting up the Domain Controller, you can now set up a client that connects to the domain.
The first step is to launch a virtual machine in Azure that has atleast 2 virtual CPUs, 8GB of memory and Windows 10. It needs to be on the same private network as your Domain Controller. 

Next, using Remote Desktop, login to your VM. Open Powershell and <code>ping</code> the Domain Controller with the IP address of the DC. 

<p>
<img src="https://i.imgur.com/ST95uBs.png" height="80%" width="80%" alt=""/>
</p>

Next, we need to set the DNS setting of the Network card of client to point to the Domain Controller. The reason for this is to make sure that when we connect our client it can reach out to the domain name that is only known within this private network. If DNS is automatically allocated to another server then it will return an error. 

In the Azure portal go to your client virtual machine, select Networking on the left-hand side then the Network card. From here select DNS servers and change it from **Inherit from Virtual Network** to **Custom**. Set the IP address to the Domain Controller.

<p>
<img src="https://i.imgur.com/cAMaElQ.png" height="80%" width="80%" alt=""/>
</p>

Next we need to actually connect the client to the Domain Controller. In your virtual machine, go to System settings by right-clicking the Start menu and selecting **System**.

<p>
<img src="https://i.imgur.com/02WVRt5.png" height="80%" width="80%" alt=""/>
</p>

Go to the bottom of the window and select **Rename this PC (advanced)**. 

<p>
<img src="https://i.imgur.com/sWuRjeF.png" height="80%" width="80%" alt=""/>
</p>

Then, select **Change** towards the bottom of the window. This will give us a prompt to connect to the domain or to a workgroup.

<p>
<img src="https://i.imgur.com/rnouL31.png" height="80%" width="80%" alt=""/>
</p>

In the **Member Of** section select **Domain**. Fill in the dialogue box with the domain address of your Domain Controller.

<p>
<img src="https://i.imgur.com/IGNqv5z.png" height="80%" width="80%" alt=""/>
</p>

You will then need to confirm that you are an administrator of the domain and can connect the client to the domain. Use you administrator credentials.

<p>
<img src="https://i.imgur.com/TrXHRPi.png" height="80%" width="80%" alt=""/>
</p>

Welcome to the Domain!!

<p>
<img src="https://i.imgur.com/7GtjbIe.png" height="80%" width="80%" alt=""/>
</p>


Once you close this window, the VM will restart. While you wait for the VM to reboot, check in your Domain Controller if the client you just connected appears in the list of Computers in **Active Directory Users and Computers**.

<p>
<img src="https://i.imgur.com/intikqN.png" height="80%" width="80%" alt=""/>
</p>

When you login back into the client, you will need to use the administrator's account. Remember to login using the <code>(domain)\(username)</code> structure.

<p>
<img src="https://i.imgur.com/tsE0ckz.png" height="80%" width="80%" alt=""/>
</p>

The final step is to allow all domain users to connect to this VM. Right-click on the Start menu again and select **System**. Then click on Remote Desktop in the left-hand menu. Then, select **Select users that can remotely access this PC**.

<p>
<img src="https://i.imgur.com/wdgLjBg.png" height="80%" width="80%" alt=""/>
</p>

Then click **Add**. And in the text area type <code>domain users</code>. Click **Check Names**. Then, **Ok** until you return to the Settings window. 

<p>
<img src="https://i.imgur.com/ZGPbs6w.png" height="80%" width="80%" alt=""/>
</p>

**Congratulations, you have connected a client and can now login as any user in the domain!!**

