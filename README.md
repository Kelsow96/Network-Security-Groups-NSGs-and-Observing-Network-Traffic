<img src="https://i.imgur.com/C11N4nJ.png" alt="Azure" width="400">

<h1> Network Security Groups (NSGs) and Using WireShark to Obeserve Network Traffic </h1>

In this tutorial, we'll be using Remote Desktop Connection (RDP) to connect to our Windows VM, use WireShark and Network Security Groups to observe network traffic between our two VMs.

<h2> Environments and Technologies Used: </h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- WireShark
- PowerShell
- Network Protocols (ICMP, SSH, DHCP, DNS, RDP)

<h2> Operating Systems Used: </h2>

-  Windows 10
-  Linux (Ubuntu)

<h2> List of Prerequisites: </h2>

-  Azure Account/Subscription
-  Previous VMs created in [Part 1](https://github.com/Kelsow96/Creating-VM-s-in-Azure-Windows-10-and-Linux-) of this project

<h2> High-Level Steps: </h2>

  1. Retreive Public IP address of our Windows 10 VM and RDP into it
  2. Download and install WireShark within Windows 10 VM
  3. Filter for ICMP traffic within WireShark
  4. Retreive Private IP address of our Linux(Ubuntu) VM and attempt to ping it from our Windows 10 VM
  5. Observe ping requests and replies within WireShark
  6. Initiate a perpetual/non-stop ping from our Windows 10 VM to our Ubuntu VM
  7. Open Network Security Groups (NSGs) witin Azure for our Linux VM and disable incoming ICMP traffic
  8. Observe ICMP traffic within WireShark and our command line window of our Windows 10 VM
  9. Re-enable ICMP traffic via NSGs within Azure for our Linux VM
  10. Observe ICMP traffic within WireShark and our command line window of our Windows 10 VM
  11. Stop ping activity
  12. Filter SSH traffic within WireShark
  13. Within our Windows 10 VM SHH into our Linux VM via its Private IP
  14. Observe SSH traffic within WireShark
  15. Exit our SSH connection
  16. 

