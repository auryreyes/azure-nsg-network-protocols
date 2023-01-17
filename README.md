<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
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

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

After creating your VMs in Azure, use Remote Desktop Connection to access the Windows virtual machine. Within your Windows 10 VM, Install Wireshark.

<h3>Step 2: Observe ICMP Traffic</h3>

Wireshark is a network protocol analyzer that can be used to see packets being captured from a network connection. Find the Linux VM's private Internet Protocol (IP) address in Azure first before continuing. Find the Linux VM's private Internet Protocol (IP) address in Azure first before continuing.

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

Internet Control Message Protocol (ICMP) is a network protocol that sends information about problems with network connectivity.

In Wireshark filter for “icmp” traffic only by typing it in the green search bar. Retrieve the private IP address of the Ubuntu VM in Azure which is (10.0.0.5). In VM1 open up powershell and try to ping the private IP address. Observe the ping requests and replies within Wireshark.

From The Windows 10 VM, open PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark.

Now set a perpetual ping using VM2’s private Ip Address following “ping -t”

Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
Disable incoming (inbound) ICMP traffic. 

Go to “VM2” in Azure Portal:
- Networking
- Add inbound port rule -> check “ICMP” -> check “Deny” -> Add

The Azure portal has Network Security Groups (NSGs). You can establish security rules for your resources, effectively creating a firewall.

Once finished, head back to the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity. Requests to time out and show no answer because ICMP traffic is being blocked.

We’ll head back to the Azure portal and re-enable ICMP traffic. You have two options: remove the rules or allow them. Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity. (should start working)

Stop the ping activity by pressing “Control” “C”

<h3>Step 2: Observe SSH Traffic</h3>

Secure Shell Protocol (SSH) is a network protocol that enables access to another machine's Command Line Interface (CLI).

Back in Wireshark, filter for SSH traffic only. Then in Powershell type “ssh” + username of VM2 “@10.0.0.5” then press [enter]

You will be prompted to log in so use your VM2 login information. Type commands (cd, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark. Exit the SSH connection by typing ‘exit’ and pressing [Enter]

<h3>Step 3: Observe DHCP Traffic</h3>

Dynamic Host Configuration Protocol (DHCP) is a network protocol that assigns an IP address to devices when they are first connected to the network.

Back in Wireshark, filter for DHCP traffic only. From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew). Observe the DHCP traffic appearing in WireShark

<h3>Step 4: Observe DNS Traffic</h3>

Domain Name System is a network protocol that converts Fully Qualified Domain Names (FQDNs) into IP addresses.

Back in Wireshark, filter for DNS traffic only. From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are. Observe the DNS traffic being show in WireShark

<h3>Step 5: Observe RDP Traffic</h3>

Remote Desktop Protocol (RDP) is used when remotely connecting from one computer to another to gain a remote desktop Graphical User Interface (GUI).

Back in Wireshark, filter for RDP traffic only (tcp.port == 3389) and observe the traffic.
Traffic is always being transmitted since the RDP (protocol) shows you a live stream from one computer to another.

<h3>!ATTENTION!</h3>

**Lab Cleanup**
- Close your Remote Desktop connection
- Delete the Resource Group(s) created at the beginning of this lab
- Verify Resource Group Deletion

Thank you for completing this tutorial. I hope you learned more about network protocols and how network traffic operates as a result.
