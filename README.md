# Observing SSH & DHCP Traffic Using Wireshark & PowerShell in Windows VM

## Part 1: Observe SSH Traffic

### Step 1: Start VMs and Ensure they are Running
- Open Azure and start VMs  
- Open Microsoft Remote Desktop and login to your Windows VM

### Step 2: Observe SSH Traffic
- Open Wireshark  
- Begin packet capture on the appropriate Ethernet interface

### Step 3: Apply SSH Filter
In Wireshark’s filter bar, type:

```
ssh
```
Press Enter to apply the filter.

![Screenshot3](images/Screenshot3.png)

### Step 4: SSH into the Ubuntu VM
- Open PowerShell as Administrator on the Windows VM  
- Enter the SSH command:

```
ssh labuser@10.0.0.5
```

![Screenshot4](images/Screenshot4.png)

### Step 5: Accept Host Key and Authenticate
- When prompted, type `yes` to accept the fingerprint  
- Enter the password for `labuser`  
- Notice that with every entry, there is SSH traffic

![Screenshot5](images/Screenshot5.png)

### Step 6: Observe SSH Traffic
Now that we are in the Ubuntu VM, we can begin to observe more SSH traffic.

![Screenshot6](images/Screenshot6.png)

### Step 7: Execute Linux Commands
Once connected to the Ubuntu VM, type the following:
```
hostname
id
uname -a
touch file.txt
```
This will create a file.

Observe that with every keystroke, there is SSH traffic.

![Screenshot7](images/Screenshot7.png)

### Step 8: Observe SSH Packet Activity in Wireshark
In the Wireshark filter bar, type:
```
tcp.port == 22
```
SSH uses TCP port 22.  
Observe the live stream of encrypted packets during the SSH session.

![Screenshot8](images/Screenshot8.png)

### Step 9: Exit the SSH Session
In PowerShell, type:
```
exit
```
Confirm the session closes and SSH traffic stops.

![Screenshot9](images/Screenshot9.png)

---

## Part 2: Observe DHCP Traffic

### Step 1: Filter for DHCP Traffic in Wireshark
In Wireshark’s filter bar, type:
```
dhcp
```
Press Enter.

![Screenshot10](images/Screenshot10.png)

### Step 2: Release & Renew IP Address via PowerShell
Open PowerShell as Administrator.  
Run the following:
```
ipconfig /renew
```

![Screenshot11](images/Screenshot11.png)

### Step 3: Automate IP Renewal with a Batch Script (Optional)
Open Notepad and type:
```
ipconfig /release
ipconfig /renew
```
Save the file as `dhcp.bat` in:
```
C:\ProgramData
```

![Screenshot12](images/Screenshot12.png)

### Step 4: Navigate to Batch Script Location
In PowerShell, type:
```
cd C:\ProgramData
ls
```

![Screenshot13](images/Screenshot13.png)

### Step 5: Run the Script to Trigger DHCP Events
Execute the script in PowerShell:
```
.\dhcp.bat
```

![Screenshot14](images/Screenshot14.png)

### Step 6: Observe DHCP Traffic in Wireshark
In Wireshark, observe the following:
- DHCP Discover  
- DHCP Offer  
- DHCP Request  
- DHCP ACK

![Screenshot15](images/Screenshot15.png)

### Step 7: Handle Temporary Disconnection
If connection drops briefly after IP release, you may see a message like:
> "Connection lost…" (temporary during IP renewal)
