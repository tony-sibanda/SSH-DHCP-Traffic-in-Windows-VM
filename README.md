Observing SSH & DHCP Traffic Using Wireshark & PowerShell in Windows VM

Part 1: Observe ssh Traffic

Step 1: 	Start VMs and Ensure they are Running

Open Azure and start VMs

Open Microsoft Remote Desktop and login to your Windows VM

Step 2:	Observe SSH Traffic

Open Wireshark.

Begin packet capture on the appropriate Ethernet interface.

Step 3: 	Apply SSH Filter


![Step 3 Screenshot](images/Screenshot3.png)


In Wireshark’s filter bar, type:
ssh

Press Enter to apply the filter.

Step 4: 	SSH into the Ubuntu VM


![Step 4 Screenshot](images/Screenshot4.png)


Open PowerShell as Administrator on the Windows VM.

Enter the SSH command:

ssh <username>@<Private IP Address>

ssh labuser@10.0.0.5

Step 5: 	Accept Host Key and Authenticate


![Step 5 Screenshot](images/Screenshot5.png)


When prompted, type yes to accept the fingerprint.

Enter the password for labuser.

Notice that with every entry there is ssh traffic.

Step 6: 	Observe ssh Traffic


![Step 6 Screenshot](images/Screenshot6.png)


Now that we are in the ubuntu vm we can begin to observe more ssh traffic.

Step 7: 	Execute Linux Commands


![Step 7 Screenshot](images/Screenshot7.png)


Once connected to the Ubuntu VM, type the following:

hostname

id

uname -a

touch file.txt this will create a file

Observe that with every key stroke there is ssh traffic

Step 8: Observe SSH Packet Activity in Wireshark


![Step 8 Screenshot](images/Screenshot8.png)


In the Wireshark filter type:
tcp.port == 22

ssh uses TCP port 22

Observe the live stream of encrypted packets during the SSH session.

Step 9: Exit the SSH Session


![Step 9 Screenshot](images/Screenshot9.png)


In PowerShell type:
exit

Confirm the session closes and SSH traffic stops.

Part 2: Observe DHCP Traffic

Step 1: Filter for DHCP Traffic in Wireshark

In Wireshark’s filter bar, type:
dhcp

Press Enter.

Step 2: Release & Renew IP Address via PowerShell

Open PowerShell as Administrator.

Run the following in PowerShell:

ipconfig /renew

Step 3: Automate IP Renewal with a Batch Script (Optional)


![Step 3 Screenshot](images/Screenshot3.png)


Open Notepad and type:
ipconfig /release

ipconfig /renew

Save the file as: dhcp.bat

Save it in: C: \ProgramData

Step 4: Navigate to Batch Script Location


![Step 4 Screenshot](images/Screenshot4.png)


In PowerShell type:
cd C: \ProgramData

ls

Step 5: Run the Script to Trigger DHCP Events


![Step 5 Screenshot](images/Screenshot5.png)


Execute the script in PowerShell:
.\dhcp.bat

Step 6: Observe DHCP Traffic in Wireshark


![Step 6 Screenshot](images/Screenshot6.png)


In Wireshark, observe the following:

DHCP Discover

DHCP Offer

DHCP Request

DHCP ACK

Step 7: Handle Temporary Disconnection


![Step 7 Screenshot](images/Screenshot7.png)


If connection drops briefly after IP release, you may see a message like: