# Observing SSH & DHCP Traffic Using Wireshark & PowerShell in Windows VM

---

## Part 1: Observe SSH Traffic

### Step 1: Start VMs and Ensure they are Running
- Open Azure and start VMs  
- Open Microsoft Remote Desktop and login to your Windows VM

---

### Step 2: Observe SSH Traffic
- Open Wireshark  
- Begin packet capture on the appropriate Ethernet interface

---

### Step 3: Apply SSH Filter  
![Step 3 Screenshot](images/Step3_SSHFilter.png)  
- In Wireshark’s filter bar, type: `ssh`  
- Press Enter to apply the filter

---

### Step 4: SSH into the Ubuntu VM  
![Step 4 Screenshot](images/Step4_SSHCommand.png)  
- Open PowerShell as Administrator on the Windows VM  
- Enter the SSH command:  
