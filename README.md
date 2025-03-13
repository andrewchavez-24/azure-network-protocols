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

- Install Wireshark
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h2>Actions and Observations</h2>

<p><b>Before getting started:</b> Create two VMs in the Azure portal: one using a Windows 10 Pro image and the other using a Linux image, each with 2 vCPUs. Ensure both VMs are attached to the same virtual network during setup. Use RDP to access the Windows machine.</p>

<h3>Install Wireshark</h3>
<p>Within your Windows 10 Virtual Machine, download and install Wireshark from https://www.wireshark.org. This tool will be used to observe network traffic.</p>
<p>
<img src="https://github.com/user-attachments/assets/608a835b-e055-4720-b67e-95c98314cb6a" height="80%" width="80%"/>
</p>

<br/>
<h3>Observe ICMP Traffic</h3>
<p>
Open Wireshark. Click "ethernet" and then click the blue shark fin at the top left corner to start capturing packets.
</p>
<p>
<img src="https://github.com/user-attachments/assets/598557b9-43d3-4e26-a405-e1f7d2db33a1" height="80%" width="80%"/>
</p>

<br/>
<p>
Open Wireshark. Click "ethernet" and then click the blue shark fin at the top left corner to start capturing packets.
</p>
<p>
<img src="https://github.com/user-attachments/assets/598557b9-43d3-4e26-a405-e1f7d2db33a1" height="80%" width="80%"/>
</p>

<br/>
<p>
Filter for ICMP traffic only
</p>
<p>
<img src="https://github.com/user-attachments/assets/4f820759-cc61-4fa0-b20a-23e17b2e213b" height="80%" width="80%"/>
</p>

<br/>
<p>
Retrieve the private IP address of the Ubuntu VM.
</p>
<p>
<img src="https://github.com/user-attachments/assets/26e7c864-d918-42e7-89b6-f4b628e24651" height="80%" width="80%"/>
</p>

<br>
<p>
Attempt to ping it from within the Windows 10 VM using Powershell.
</p>
<p>
<img src="https://github.com/user-attachments/assets/aa96111a-e984-4d4c-942f-ecc680478019" height="80%" width="80%"/>
</p>

<br>
<p>
Observe ping requests and replies within WireShark
</p>
<p>
<img src="https://github.com/user-attachments/assets/e09d325e-5021-4d76-95f2-ed3e10a3c0fc" height="80%" width="80%"/>
</p>

<br>
<h3>Configuring a Firewall [Network Security Group]</h3>
<p>
Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM by typing "ping (IP Address) -t" in powershell.
</p>
<p>
<img src="https://github.com/user-attachments/assets/647467ba-3ff8-4544-bbb7-a2ed74bfe080" height="80%" width="80%"/>
</p>

<br>
<p><b>Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic.</b></p>
<p>Go to virtual machines in Azure, click linux-vm, click the Networking drop down, click Network settings, then click the link under Network security group. Select the Settings dropdown, click Inbound security rules, click +Add, put an asterick in the Destination port ranges, select ICMPv4 protocol, select Deny Action, set priority to 290, then click Add.
</p>
<p>
<img src="https://github.com/user-attachments/assets/b95b0572-bacf-41fe-8185-6c4e1c6b2ecd" height="80%" width="80%"/>
</p>

<br>
<p>Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
</p>
<p>
<img src="https://github.com/user-attachments/assets/b95b0572-bacf-41fe-8185-6c4e1c6b2ecd" height="80%" width="80%"/>
</p>

