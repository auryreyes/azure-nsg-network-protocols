<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (ICMP, SSH, DHCP, DNS, RDP))
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create VMs & Download Wireshark
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h2>Actions and Observations</h2>
<h3>!ATTENTION!</h3>

Before we begin, if you haven’t already created an Azure Account or don’t know how to create a VM please refer to my [tutorial](https://github.com/auryreyes/create-azure-virtual-machine).

<h3>Step 1: Create VMs & Download Wireshark</h3>

We have to create two virtual machines (VMs) in Azure.
- Create Resource Group
- Create Windows 10 Virtual Machine (VM)
- Create a Linux (Ubuntu) VM

After creating your VMs in Azure, use Remote Desktop Connection to access the Windows virtual machine. Within your Windows 10 VM, Install Wireshark.

Wireshark is a network protocol analyzer that can be used to see packets being captured from a network connection. Find the Linux VM's private Internet Protocol (IP) address in Azure first before continuing. Find the Linux VM's private Internet Protocol (IP) address in Azure first before continuing.

<p>
<img src="https://i.imgur.com/aoq1txh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/GQnEboB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<h3>Step 2: Observe ICMP Traffic</h3>

Internet Control Message Protocol (ICMP) is a network protocol that sends information about problems with network connectivity.

**ICMP**
- In Wireshark filter for “icmp” traffic only by typing it in the green search bar
- Retrieve the private IP address of the Ubuntu VM in Azure which is (10.0.0.5)
- In VM1 open up powershell and try to ping the private IP address. Observe the ping requests and replies within Wireshark

<p>
<img src="https://i.imgur.com/Yqx7XvH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/HgY0Tsm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/GFD1TC3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

From The Windows 10 VM, open PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark.

<p>
<img src="https://i.imgur.com/dlXJ8BV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

Now set a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM using Ubuntu VM’s private Ip Address following “ping -t”

<p>
<img src="https://i.imgur.com/xHRo2lY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

The Azure portal has Network Security Groups (NSGs). You can establish security rules for your resources, effectively creating a firewall.

Disable incoming (inbound) ICMP traffic
- Head to “Network Security Groups” in Azure Portal
- Select “VM2-nsg”
- Click “Inbound security rules”
- Add inbound port rule -> check “ICMP” -> check “Deny” -> Add
- Priority: 200
- Name: DENY_ICMP_FROM_ANYWHERE

<p>
<img src="https://i.imgur.com/MOFH5t6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/dbd5fmO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/hMUnXCF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/5bQP6hJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

Once finished, head back to the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity. Requests to time out and show no answer because ICMP traffic is being blocked.

<p>
<img src="https://i.imgur.com/JjJZipV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

We’ll head back to the Azure portal and re-enable ICMP traffic. You have two options: remove the rules or allow them. Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working).

<p>
<img src="https://i.imgur.com/9beAIwh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/UAJiyb4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/s30fXN8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

Stop the ping activity by pressing “Control + C”

<p>
<img src="https://i.imgur.com/hpa0XJT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<h3>Step 2: Observe SSH Traffic</h3>

Secure Shell Protocol (SSH) is a network protocol that enables access to another machine's Command Line Interface (CLI).

**SSH**
- Back in Wireshark, filter for SSH traffic only. 
- Then in Powershell type “ssh” + username of VM2 “@10.0.0.5” then press [Enter]. 
- You will be prompted to log in so use your VM2 login information. Type commands (cd, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark. 
- Exit the SSH connection by typing ‘exit’ and pressing [Enter].

<p>
<img src="https://i.imgur.com/LFgsXiE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/Cq1sa2S.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<h3>Step 3: Observe DHCP Traffic</h3>

Dynamic Host Configuration Protocol (DHCP) is a network protocol that assigns an IP address to devices when they are first connected to the network.

**DHCP**
- Back in Wireshark, filter for DHCP traffic only. 
- From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew). Observe the DHCP traffic appearing in WireShark.

<p>
<img src="https://i.imgur.com/WzwYmLT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<h3>Step 4: Observe DNS Traffic</h3>

Domain Name System is a network protocol that converts Fully Qualified Domain Names (FQDNs) into IP addresses.

**DNS**
- Back in Wireshark, filter for DNS traffic only. 
- From your Windows 10 VM within a command line, use nslookup to see google.com's IP address. Observe the DNS traffic being shown in WireShark.

<p>
<img src="https://i.imgur.com/b7y2zXR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<h3>Step 5: Observe RDP Traffic</h3>

Remote Desktop Protocol (RDP) is used when remotely connecting from one computer to another to gain a remote desktop Graphical User Interface (GUI).

**RDP**
- Back in Wireshark, filter for RDP traffic only (tcp.port == 3389) and observe the traffic. 

Traffic is always being transmitted since the RDP (protocol) shows you a live stream from one computer to another.

<p>
<img src="https://i.imgur.com/NtIlOa8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<h3>!ATTENTION!</h3>

Because the majority of Azure services are pay-as-you-go, be sure to remove ALL resource groups and virtual machines if you want to keep your free $200 credits.

Thank you for completing this tutorial! I hope you learned more about network protocols and how network traffic operates as a result.
