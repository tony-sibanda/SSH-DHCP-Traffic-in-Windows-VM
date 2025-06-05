# Observing SSH & DHCP Traffic Using Wireshark & PowerShell in Windows VM

## Part 1: Observe SSH Traffic

### Step 1: Start VMs and Ensure they are Running
Open Azure and start VMs  
Open Microsoft Remote Desktop and login to your Windows VM

### Step 2: Observe SSH Traffic
Open Wireshark  
Begin packet capture on the appropriate Ethernet interface

### Step 3: Apply SSH Filter  
In Wireshark’s filter bar, type:  
```bash
ssh
```
![Wireshark SSH Filter](images/Screenshot2.png)

### Step 4: SSH into the Ubuntu VM  
Open PowerShell as Administrator on the Windows VM  
Enter the SSH command:  
```bash
ssh labuser@10.0.0.5
```
![SSH Command](images/Screenshot1.png)

### Step 5: Accept Host Key and Authenticate  
When prompted, type `yes` to accept the fingerprint  
Enter the password for `labuser`  
Notice that with every entry there is SSH traffic  
![Accept SSH Fingerprint](images/Screenshot10.png)

### Step 6: Observe SSH Traffic  
Now that we are in the ubuntu vm we can begin to observe more ssh traffic

### Step 7: Execute Linux Commands  
Once connected to the Ubuntu VM, type the following:
```bash
hostname
id
uname -a
touch file.txt  # this will create a file
```
Observe that with every keystroke there is ssh traffic  
![Execute Commands](images/Screenshot4.png)

### Step 8: Observe SSH Packet Activity in Wireshark  
In the Wireshark filter type:  
```bash
tcp.port == 22
```
SSH uses TCP port 22  
Observe the live stream of encrypted packets during the SSH session  
![TCP Port 22 Filter](images/Screenshot6.png)  
![Observe SSH Packets](images/Screenshot7.png)

### Step 9: Exit the SSH Session  
In PowerShell type:  
```bash
exit
```
Confirm the session closes and SSH traffic stops  
![Exit SSH](images/Screenshot9.png)

---

## Part 2: Observe DHCP Traffic

### Step 1: Filter for DHCP Traffic in Wireshark  
In Wireshark’s filter bar, type:  
```bash
dhcp
```
Press Enter  
![DHCP Filter](images/Screenshot5.png)

### Step 2: Release & Renew IP Address via PowerShell  
Open PowerShell as Administrator  
Run the following in PowerShell:  
```bash
ipconfig /renew
```
![IP Config Renew](images/Screenshot11.png)

### Step 3: Automate IP Renewal with a Batch Script (Optional)  
Open Notepad and type:  
```bash
ipconfig /release
ipconfig /renew
```
Save the file as: `dhcp.bat`  
Save it in: `C:\ProgramData`  
![Batch Script Creation](images/Screenshot3.png)

### Step 4: Navigate to Batch Script Location  
In PowerShell type:  
```bash
cd C:\ProgramData
ls
```
![Navigate to Script](images/Screenshot13.png)

### Step 5: Run the Script to Trigger DHCP Events  
Execute the script in PowerShell:  
```bash
.\dhcp.bat
```
![Run Script](images/Screenshot12.png)

### Step 6: Observe DHCP Traffic in Wireshark  
In Wireshark, observe the following:
- DHCP Discover  
- DHCP Offer  
- DHCP Request  
- DHCP ACK  
![Observe DHCP Packets](images/Screenshot15.png)

### Step 7: Handle Temporary Disconnection  
If connection drops briefly after IP release, you may see a message like:  
![Reconnect VM](images/Screenshot14.png)
