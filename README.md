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
