# How to configure Virtual Local Area Network VLAN
<img width="1317" height="642" alt="image" src="https://github.com/user-attachments/assets/7897d8ae-172c-45e6-8fda-c615632c3bed" />

## Step 1: Basic configuration on switches
### SW1
```
enable
configure terminal
hostname SW1
no ip domain-lookup
enable secret cisco123
service password-encryption
line console 0
password cisco
login
exit
```

### SW2
```
enable
configure terminal
hostname SW2
no ip domain-lookup
enable secret cisco123
service password-encryption
line console 0
password cisco
login
exit
```

### SW3
```
enable
configure terminal
hostname SW3
no ip domain-lookup
enable secret cisco123
service password-encryption
line console 0
password cisco
login
exit
```

## step 2: Create VLAN
### SW1
```
enable
configure terminal
vlan 10
name Student
vlan 20
name IT
vlan 30
name Teacher
end
```

### SW2
```
enable
configure terminal
vlan 10
name Student
vlan 20
name IT
vlan 30
name Teacher
end
```
### SW3
```
enable
configure terminal
vlan 10
name Student
vlan 20
name IT
vlan 30
name Teacher
end
```
## Assign VLAN to ports
### SW1

```
configure terminal
interface fastEthernet0/1
switchport mode access
switchport access vlan 10

configure terminal
interface fastEthernet0/2
switchport mode access
switchport access vlan 20

configure terminal
interface fastEthernet0/3
switchport mode access
switchport access vlan 30
```

### SW3

```
configure terminal
interface fastEthernet0/3
switchport mode access
switchport access vlan 10

configure terminal
interface fastEthernet0/2
switchport mode access
switchport access vlan 20

configure terminal
interface fastEthernet0/3
switchport mode access
switchport access vlan 10
```
## Configure Trunk port
### SW1

```
configure terminal
interface Giga0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30
```

### SW2

```
configure terminal
interface Giga0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30

configure terminal
interface Giga0/2
switchport mode trunk
switchport trunk allowed vlan 10,20,30
```
### SW3

```
configure terminal
interface Giga0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30
```
