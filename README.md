###Homework 2 - Basic switch configuration
Here is a complete, step-by-step guide to setting up and configuring this topology in Cisco Packet Tracer.

---

# Cisco Networking Lab Guide: Basic Config, Telnet, and SSH

This guide covers the physical setup, IP addressing, basic switch security, and remote management (Telnet & SSH) for a three-switch network.

---

## Step 1: Physical Topology Setup
Add the following devices in Cisco Packet Tracer and connect them using the specified cables:

*   **Switches:** Three **2960 Switches** (Rename them **SW1**, **SW2**, and **SW3**).
*   **PCs:** Five PCs (Rename them **PC0** to **PC4**).

### Cabling Connections:
*   **SW1 Connections:**
    *   `Fa0/1` to `PC0` (`Fa0`) — *Copper Straight-Through*
    *   `Fa0/2` to `PC1` (`Fa0`) — *Copper Straight-Through*
    *   `Fa0/3` to `SW2` `Fa0/1` — *Copper Cross-Over (dashed line)*
*   **SW2 Connections:**
    *   `Fa0/2` to `PC2` (`Fa0`) — *Copper Straight-Through*
    *   `Fa0/3` to `SW3` `Fa0/1` — *Copper Cross-Over (dashed line)*
*   **SW3 Connections:**
    *   `Fa0/2` to `PC3` (`Fa0`) — *Copper Straight-Through*
    *   `Fa0/3` to `PC4` (`Fa0`) — *Copper Straight-Through*

---

## Step 2: Configure IP Addresses on the PCs
Click on each PC, go to **Desktop** -> **IP Configuration**, and set the static IP and Subnet Mask:

*   **PC0:** IP `192.168.1.10` | Subnet Mask `255.255.255.0`
*   **PC1:** IP `192.168.1.20` | Subnet Mask `255.255.255.0`
*   **PC2:** IP `192.168.1.30` | Subnet Mask `255.255.255.0`
*   **PC3:** IP `192.168.1.50` | Subnet Mask `255.255.255.0`
*   **PC4:** IP `192.168.1.40` | Subnet Mask `255.255.255.0`

---

## Step 3: Switch Configurations (SW1, SW2, SW3)
Double-click each switch, navigate to the **CLI** tab, press Enter to start, and copy-paste the configuration block for each device.

### Switch 1 (SW1) Configuration:
```text
enable
configure terminal
hostname SW1

# 1. Console Port Security
line console 0
 password cisco123
 login
 exit

# 2. Privileged Mode Password
enable secret admin123

# 3. Management IP Address
interface vlan 1
 ip address 192.168.1.1 255.255.255.0
 no shutdown
 exit

# 4. SSH Prerequisites
ip domain-name local.lan
username admin privilege 15 secret admin123
crypto key generate rsa
```
*(When prompted for the key modulus size, type **`1024`** and press Enter)*

```text
ip ssh version 2

# 5. Remote Access (VTY Lines for Telnet & SSH)
line vty 0 15
 login local
 transport input all
 exit
exit

# Save configuration
write memory
```

---

### Switch 2 (SW2) Configuration:
```text
enable
configure terminal
hostname SW2

# 1. Console Port Security
line console 0
 password cisco123
 login
 exit

# 2. Privileged Mode Password
enable secret admin123

# 3. Management IP Address
interface vlan 1
 ip address 192.168.1.2 255.255.255.0
 no shutdown
 exit

# 4. SSH Prerequisites
ip domain-name local.lan
username admin privilege 15 secret admin123
crypto key generate rsa
```
*(When prompted for the key modulus size, type **`1024`** and press Enter)*

```text
ip ssh version 2

# 5. Remote Access (VTY Lines for Telnet & SSH)
line vty 0 15
 login local
 transport input all
 exit
exit

# Save configuration
write memory
```

---

### Switch 3 (SW3) Configuration:
```text
enable
configure terminal
hostname SW3

# 1. Console Port Security
line console 0
 password cisco123
 login
 exit

# 2. Privileged Mode Password
enable secret admin123

# 3. Management IP Address
interface vlan 1
 ip address 192.168.1.3 255.255.255.0
 no shutdown
 exit

# 4. SSH Prerequisites
ip domain-name local.lan
username admin privilege 15 secret admin123
crypto key generate rsa
```
*(When prompted for the key modulus size, type **`1024`** and press Enter)*

```text
ip ssh version 2

# 5. Remote Access (VTY Lines for Telnet & SSH)
line vty 0 15
 login local
 transport input all
 exit
exit

# Save configuration
write memory
```

---

## Step 4: Verification and Testing

To confirm everything works, open the **Command Prompt** on any PC (such as **PC0**) and test the following commands:

### 1. Test Network Connectivity (Ping)
Verify you can reach Switch 1:
```cmd
ping 192.168.1.1
```
*(Note: It is normal for the very first ping request to time out while the ARP table resolves. The subsequent requests should succeed.)*

### 2. Test Secure Shell Access (SSH)
Connect to Switch 1 securely:
```cmd
ssh -l admin 192.168.1.1
```
*   **Password:** `admin123`
*   Once logged in, type `enable` and enter the enable secret password `admin123` to reach privileged configuration mode.
*   Type `exit` to disconnect.

### 3. Test Telnet Access
Connect to Switch 1 via Telnet:
```cmd
telnet 192.168.1.1
```
*   **Username:** `admin`
*   **Password:** `admin123`
*   Type `exit` to disconnect.
