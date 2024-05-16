<img src="https://i.imgur.com/C11N4nJ.png" alt="Azure" width="400">

<h1> Network Security Groups (NSGs) and Using WireShark to Observe Network Traffic </h1>

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

  1. Retrieve Public IP address of our Windows 10 VM and RDP into it
  2. Download and install WireShark within Windows 10 VM
  3. Filter for ICMP traffic within WireShark
      -  Retrieve Private IP address of our Linux(Ubuntu) VM and attempt to ping it from our Windows 10 VM
      -  Observe ping requests and replies within WireShark
      -  Initiate a perpetual/non-stop ping from our Windows 10 VM to our Linux VM
      -  Open Network Security Groups (NSGs) within Azure for our Linux VM and disable incoming ICMP traffic
      -  Observe ICMP traffic within WireShark and our command line window of our Windows 10 VM
      -  Re-enable ICMP traffic via NSGs within Azure for our Linux VM
      -  Observe ICMP traffic within WireShark and our command line window of our Windows 10 VM
      -  Stop ping activity
  4. Filter SSH traffic within WireShark
      - Within our Windows 10 VM SHH into our Linux VM via its Private IP
      - Observe SSH traffic within WireShark
      - Exit our SSH connection
  5. Filter for DHCP traffic within WireShark
      - Within our Windows 10 VM command line, attempt to issue a new IP address with ipconfig/renew
      - Observe DHCP traffic within WireShark
  7. Filter for DNS traffic within WireShark
      - Within our Windows 10 VM command line, use nslookup to see what google.com's ip address is
      - Observe DNS traffic within WireShark
  9. Filter for RDP traffic within WireShark
      - Within WireShark, use tcp.port == 3389 to filter for RDP traffic
      - Observe DNS traffic within WireShark
    

<h2> Steps: </h2>

  1. We first need to retrieve our Windows 10 VMs public IP address to RDP into it.
![Capture](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/ddb5e216-b240-4481-a5e0-38827447f647)
![image](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/8ff956ea-3bab-4b39-8c39-f8da935b859c)
  <br>
  <br/>
  
-  Next we'll use the credentials we created in the first part of this lab to log into our Windows 10 VM.
    - Username: Jane
    - Password: Password1234 <br> <br/>
![Capture](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/ad1f3e35-faf5-4fd8-b126-757cec80a3d7)
  <br>
  <br/>

  2. Once we're inside our Windows 10 VM, we'll download and install WireShark.
![image](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/ff3a4f37-cd88-4ef2-8446-df86f8120423)
![image](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/4968374b-c947-4ffc-bd06-28454e8b709c)
  <br>
  <br/>
  
  3. Once we have WireShark installed, we'll open the application and filter for ICMP traffic.
![image](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/abe7b637-cf97-4513-b1cb-b18d3863bae0)
  <br>
  <br/>
  
-  We'll now retrieve the private IP address of our Linux(Ubuntu) VM and attempt to ping it from our Windows 10 VM using PowerShell.
![Capture](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/9716b4f8-0c30-480a-93cd-d3eeff657947)

- We see that within both PowerShell and WireShark we have succesefully pinged our Linux VM from our Windows VM anc received replies
![image](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/b74f93bb-bf10-44a8-b15d-8981a19b395c)

- We'll now initiate a perpetual ping from our Windows VM to our Linux VM. We'll then notice that our Windows VM will continually send ping requests and will continually receive replies from our Linux VM forever until we tell it to stop or implement security rules for one of our VMs to block ICMP traffic.
![image](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/6cee7034-2b27-4adf-95fc-feed452e3a9d)

- We'll block ICMP traffic for our Linux VM by using Network Security Groups (NSGs) within Azure with an inbound rule.
![Capture](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/aafc828b-6abb-4464-8ff2-6b358f2644e0)
![Capture](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/7f77f55d-afeb-434b-83bc-9691b500ea09)
![Capture](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/cacb4d69-22f2-42fe-9dcd-4f001e7a2811)
![Capture](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/822c36db-b066-4207-a7cd-acb549b38fbd)

- We notice after some time for the rule to take effect that our Windows 10 VM is no longer receiving replies from our Linux VM. That's because we've blocked all requests ping requests using the block ICMP rule via Network Security Groups.
![Capture](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/19dfb78c-e798-42fd-b915-274fafb61562)

- We'll go back into our NSG panel and re-allow ICMP traffic for our Linux VM.
![Capture](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/6ade365f-a875-467c-bc0a-1323eec6cfcb)
![Capture](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/d2602754-0904-4159-aa45-43b66118a034)

- We notice after some time for the rule to take effect that our Windows 10 VM is now receiving replies from our Linux VM. That's because we've re-allowed ICMP traffic for our Linux VM via Network Security Groups. 
![Capture](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/2b5cccb8-0507-4e61-ae67-6bce93b19627)

- We can now stop our perpetual ping by pressing "ctrl + c" in our Powershell window.
![image](https://github.com/Kelsow96/Network-Security-Groups-NSGs-and-Observing-Network-Traffic/assets/169297569/aa063e16-77d9-4b0f-a13f-7756afdb0c7a)





