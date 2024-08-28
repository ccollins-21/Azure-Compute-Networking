<h1>Azure Compute and Networking</h1>

 ### [YouTube Demonstration](https://youtu.be)

<h2>Description</h2>
Project consists of creating virtual machines and a network where I monitor netowrk traffic with software called Wireshark. This is all done within Microsoft Azure. 
<br />


<h2>Enviroments and Utilities Used</h2>

- <b>Microsoft Azure</b>
- <b>Virtual Machines</b>
- <b>Remote Desktop Connection</b> 
- <b>Wireshark</b>
- <b>Various Network Protocols (ICMP, SSH, DHCP, DNS)</b>
- <b>Command-Line Tools</b>

<h2>Operating Systems Used </h2>

- <b>Windows 10</b>
- <b>Ubuntu 24.04</b>

<h2>Project Walk-Through:</h2>

<p align="center">
Navigate to Microsoft Azure and create a resource group: <br/>
<img src="https://i.imgur.com/Nq0B5A5.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Once my resource group is created, next I'll create the first virtual machine:  <br/>
<img src="https://i.imgur.com/aYzQfAh.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Setting up the first virtual machine:  <br/>
<img src="https://i.imgur.com/i5ztDtu.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
<img src="https://i.imgur.com/brgIyMT.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
I'll leave all other settings to default and create this VM:  <br/>
<img src="https://i.imgur.com/OrrgUQv.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Now Azure has set up a VM, an IP for the VM, a network security group, a virtual network, a disk, and a NIC (Network Interface Card):  <br/>
<img src="https://i.imgur.com/gIWv0pv.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Second VM setup:  <br/>
<img src="https://i.imgur.com/vfUOJaG.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
<img src="https://i.imgur.com/keOWo28.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
In the "Networking" tab I want to make sure this VM will be on the same virtual network as the first one I made. So, I'll select the one already made for "VM1" instead of creating a new virtual network:  <br/>
<img src="https://i.imgur.com/QXLXthz.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Now if I go back to my resource group we can see that Azure created everything for VM2 as it did for VM1. Notice how there is only one network, however. This is because the two VMs are on the same network:  <br/>
<img src="https://i.imgur.com/gIWv0pv.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
I use VM1's public IP to connect to it using RDP:  <br/>
<img src="https://i.imgur.com/uBvHBXK.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Once my computer has connected to VM1 I will download Wireshark on the VM:  <br/>
<img src="https://i.imgur.com/lfj12DA.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Once Wireshark has downloaded and opened I will select "Ethernet" to observe network traffic:  <br/>
<img src="https://i.imgur.com/qCIJYSG.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
To filter for ICMP traffic I type "ICMP" at the top of wireshark. To make traffic I will get the private IP address of VM2 and ping it from PowerShell:  <br/>
<img src="https://i.imgur.com/gFeHSRf.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
<img src="https://i.imgur.com/MG6FzdI.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Now we can make some firewall configurations to deny any ICMP traffic. To do this I will enter a perpetual ping command into PowerShell:  <br/>
<img src="https://i.imgur.com/HGNy9PE.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Next I will go to VM2's network security group and create a new inbound security rule denying all ICMP traffic making sure to put its priorty highest, so it will take precedence before all other rules:  <br/>
<img src="https://i.imgur.com/H2zVFyt.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Going back to our VM we can see that the ICMP echo requests aren't getting any responses due to the security change:  <br/>
<img src="https://i.imgur.com/MoFJ39C.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
To revert the change I can either switch the inbound rule to "Allow" instead of "Deny" or delete the rule:  <br/>
<img src="https://i.imgur.com/4tetl2l.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Now ICMP echo requests are back to getting responses:  <br/>
<img src="https://i.imgur.com/FPXmXdY.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Now I will filter to only show SSH traffic by typing SSH into the bar at the top and I will SSH into VM2 using PowerShell:  <br/>
<img src="https://i.imgur.com/blrFX07.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
I can type commands like pwd and observe the traffic:  <br/>
<img src="https://i.imgur.com/Corgjvn.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
After filtering for DHCP traffic, I attemped to get a new IP address by using the ipconfig /renew command:  <br/>
<img src="https://i.imgur.com/Zq7X1Zv.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Filtering for DNS traffic, I can use nslookup to find IP addresses for domain names like "www.google.com" and "www.amazon.com":  <br/>
<img src="https://i.imgur.com/3cGR7xZ.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Finally, I'll observe a livestream of RDP traffic by typing in "tcp.port == 3389" in the top bar:  <br/>
<img src="https://i.imgur.com/0eQAkky.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
