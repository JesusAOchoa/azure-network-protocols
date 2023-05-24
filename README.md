<p align="center">
<img src="https://imgur.com/y5qHXey.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
This tutorial explores network traffic analysis for Azure Virtual Machines using Wireshark and experiments with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (ICMP, SSH, DHCP, DNS, RDP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>List Format</h2>

- Step 1:Let's begin by setting up a Resource Group and deploying two Virtual Machines (VM) in Microsoft Azure. One VM will be running Windows 10, while the other will be running Ubuntu.
- Step 2:To establish a connection with our Windows 10 Virtual Machine, we will utilize Remote Desktop. Once connected, we can proceed to install Wireshark. 
- Step 3:Launch Wireshark and apply a filter to display only ICMP traffic. Obtain the private IP address of the Ubuntu VM and initiate a ping from the Windows 10 VM to the Ubuntu VM. Monitor the ping requests and replies within Wireshark to observe the network activity.
- Step 4: Start an uninterrupted ping from your Windows 10 VM to your Ubuntu/Linux VM. Access the Network Security Group associated with your Ubuntu VM and deactivate the incoming (inbound) ICMP traffic. Return to the Windows 10 VM and analyze the ICMP traffic within Wireshark, as well as monitor the command line ping activity.
Re-enable ICMP traffic for the Network Security Group assigned to your Ubuntu VM. Return to the Windows 10 VM and analyze the ICMP traffic within Wireshark while also monitoring the command line ping activity. You should observe that the ping activity has resumed successfully. Finally, stop the ongoing ping activity.
- Step 5: Using your Windows 10 VM, establish an SSH connection to your Ubuntu Virtual Machine by using its private IP address. Once connected, observe the network traffic within Wireshark. After observing the traffic, exit the SSH session.
- Step 6:In your Windows 10 VM, try renewing the IP address by using the command line command "ipconfig /renew." While performing this action, monitor the DHCP traffic within Wireshark to observe the network activity.
- Step 7: Within the command line of your Windows 10 VM, execute the "nslookup" command to retrieve information about "nike.com" and observe the DNS traffic within Wireshark.
- Step 8: Observe all of the ongoing RDP traffic (tcp.port == 3389) in Wireshark
- Clean up and delete all made resources in order to not eat up your Azure credit.

<h2>Actions and Observations</h2>
<p>
<p>

<h3>Step 1: Create Resource Groups and Virtual Machines</h3>
One of the requierement for this lab is to create our Resource Group and two (2) VMs on Azure. One machine will be a Windows 10 (VM1) and the other will be a Linux machine (VM2).<br/>

<p></p>


<p></p>

<p></p>


<img src="https://i.imgur.com/jIrniNI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<h3>Step 2: Download Wireshark via RDP on Windows Virtual Machine (VM1) </h3>
<p></p>

Use Remote Desktop to connect to our Windows 10 Virtual Machine (VM1) using the Public IP address and Install [Wireshark](https://www.wireshark.org/download.html) in there.
<p

<p></p>

<img src="https://i.imgur.com/Vq6wpon.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<h3>Step 3: Observe ICMP Traffic</h3>
Once Wireshark downloaded and Installed in Windows 10 VM (VM1), I opened and filtered for ICMP traffic only. Then using Powershell and the private IP address of the Ubuntu VM (VM2) I attempted to ping it from within the Windows 10 VM and Observed ping requests and replies within Wireshark from both Virtual Machines.

<br />
<p>
</p>
<p>
<h3>Step 4: </h3>
<p></p>
 
Now, after I Initiated a perpetual/non-stop ping from our Windows 10 VM to our Ubuntu/Linux VM, let's Open the Network Security Group using by the Ubuntu VM, disable incoming (inbound) ICMP traffic and observe the ICMP traffic in WireShark and the command line Ping activity.
<br/>
<img src="https://i.imgur.com/VLuPiCJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
Observe the ping request times out after the firewall rule was put in place (*note - The ping request timed out due to the ICMP traffic being denied as the firewall rule blocked the traffic).
<br />

</p>
<p>
Back to VM2’s Network Security Group to "Allow" the Inbound Security Rule that was set up to deny so the incoming ICMP traffic would be allowed to VM2 again. We can see that Re-enable ICMP traffic for the Network Security Group in Ubuntu VM bring back ping requests and replies within wireshark. Now we can stop the ping activity by preessing "Control" + "C".
<br />
<img src="https://i.imgur.com/Tcu7L1u.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<h3>Step 5: Observe SSH Traffic </h3>
<p></p>  
  
I then filtered for SSH (Secure Shell) traffic in Wireshark and used the PowerShell terminal to “SSH into” VM2. Connecting to VM2 using SSH, along with typing and executing commends, generated SSH packets that could be observed in Wireshark. Using the “exit” command to end the SSH session.
<br />
<img src="https://i.imgur.com/gD7kvlG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
<h3>Step 6: Observe DHCP Traffic </h3>
<p></p>
 
To observe DHCP (Dynamic Host Configuration Protocol) traffic which is the network protocol responsible for automatically assigning IP addresses, let's filter for DHCP traffic in Wireshark and used the “ipconfig /renew” command to attempt to issue a new IP address to VM1. Although the private IP address did not change, Wireshark shows that there was a request and acknowledgement, so DHCP traffic was generated.
<br />
<img src="https://i.imgur.com/1COIRiA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
<h3>Step 7: Observe DNS Traffic </h3>
<p></p>
In Wireshark, I filtered for DNS (Domain Name System)  traffic and used the “nslookup” command for www.nike.com. This command basically asks our DNS server what is nike's IP address. DNS is the network protocol that transforms Fully Qualified Domain Names (FQDNs) into their assigned IP addresses.
<br />
<p>
<h3>Step 8: Observe RDP Traffic </h3>
<p></p>
 Finally, I will filter for RDP (Remote Desk Protocol) traffic by using the TCP port number (tcp.port==3389). RDP is the protocol that allows the remote connection to another computer and complete control of the Graphical User Interface (GUI). RDP traffic was continually generated 
<br />
</p>
Thank you for checking out this tutorial. It should have helped you gain a better understanding of network protocols and how network traffic works.


**REMEMBER TO DELETE YOUR RESOURCES AS TO NOT EAT UP YOUR CREDIT  **
