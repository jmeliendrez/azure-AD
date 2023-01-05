# ✍️ Creating DNS Records
After setting up 2 VMs, I begin filtering traffic using WireShark to then look at and analyse.

<h2>Video Demonstration</h2>

- ### [YouTube: Creating DNS records in Active Directory]()

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Microsoft Remote Desktop
- Wireshark

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10

<h2>List of Prerequisites</h2>

- Networked Virtual Machines
- Server set to Domain Controller
- Active Directory installed on Server
- Client connected to Domain Controller

<h2>Project Steps</h2>



<p>
<img src="https://i.imgur.com/MFk1JTO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

## A-Record Creation and Testing
Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)

Connect/log into Client-1 as an admin (mydomain\jane_admin)

From Client-1 try to ping “mainframe” notice that it fails

Nslookup “mainframe” notice that it fails (no DNS record)

Create a DNS A-record on DC-1 for “mainframe” and have it point to DC-1’s Private IP address

Go back to Client-1 and try to ping it. Observe that it works

## Local DNS Cache
Local DNS cache is the saved records that are located on your local machine. When a request is made to resolve a name to an IP address, your machine will check the local cache first to see if a record exists. If not it will then reach out to the hosts file. If that fails, it will ask the DNS server. The local cache at times needs to be flushed to make way for updated records. Below I demonstrate this fact using the record we created above.

Go back to DC-1 and change mainframe’s record address to 8.8.8.8

Go back to Client-1 and ping “mainframe” again. Observe that it still pings the old address

Observe the local dns cache (ipconfig /displaydns)

Flush the DNS cache (ipconfig /flushdns). Observe that the cache is empty

Attempt to ping “mainframe” again. Observe the address of the new record is showing up

## CNAME Record Creation and Testing
Go back to DC-1 and create a CNAME record that points the host “search” to “www.google.com”

Go back to Client-1 and attempt to ping “search”, observe the results of the CNAME record

On Client-1, nslookup “search”, observe the results of the CNAME record

