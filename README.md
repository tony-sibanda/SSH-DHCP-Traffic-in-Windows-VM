# Observing SSH & DHCP Traffic Using Wireshark & PowerShell in Windows VM

---

## Part 1: Observe SSH Traffic

---

### Step 1: Start VMs and Ensure They Are Running

- Open Azure and start both VMs.
- Open Microsoft Remote Desktop and log in to your Windows VM.

---

### Step 2: Observe SSH Traffic

- Open **Wireshark**.
- Begin packet capture on the appropriate Ethernet interface.

![Screenshot](images/Screenshot1.png)

---

### Step 3: Apply SSH Filter

- In Wireshark’s filter bar, type:
  ```
  ssh
  ```
- Press Enter to apply the filter.

![Screenshot](images/Screenshot2.png)

---

### Step 4: SSH into the Ubuntu VM

- Open **PowerShell as Administrator** on the Windows VM.
- Enter the SSH command:
  ```
  ssh labuser@10.0.0.5
  ```

![Screenshot](images/Screenshot3.png)

---

### Step 5: Accept Host Key and Authenticate

- When prompted, type `yes` to accept the fingerprint.
- Enter the password for `labuser`.
- Notice that with every entry, there is SSH traffic.

![Screenshot](images/Screenshot4.png)

---

### Step 6: Observe SSH Traffic

- Now that you are in the Ubuntu VM, observe the SSH traffic generated.

![Screenshot](images/Screenshot5.png)

---

### Step 7: Execute Linux Commands

- Type the following commands:
  ```
  hostname
  id
  uname -a
  touch file.txt
  ```
- Each keystroke and command triggers SSH traffic.

![Screenshot](images/Screenshot6.png)

---

### Step 8: Observe SSH Packet Activity in Wireshark

- In the Wireshark filter, type:
  ```
  tcp.port == 22
  ```
- SSH uses **TCP port 22**.
- Observe the encrypted packets during the session.

![Screenshot](images/Screenshot7.png)

---

### Step 9: Exit the SSH Session

- In PowerShell, type:
  ```
  exit
  ```
- Confirm the session closes and SSH traffic stops.

![Screenshot](images/Screenshot8.png)

---

## Part 2: Observe DHCP Traffic

---

### Step 1: Filter for DHCP Traffic in Wireshark

- In Wireshark’s filter bar, type:
  ```
  dhcp
  ```
- Press Enter.

![Screenshot](images/Screenshot9.png)

---

### Step 2: Release & Renew IP Address via PowerShell

- Open PowerShell as Administrator.
- Run the command:
  ```
  ipconfig /renew
  `
