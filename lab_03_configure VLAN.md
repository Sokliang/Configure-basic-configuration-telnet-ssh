# How to configure Virtual Local Area Network VLAN
<img width="1317" height="642" alt="image" src="https://github.com/user-attachments/assets/7897d8ae-172c-45e6-8fda-c615632c3bed" />

## Step 1: Basic configuration on switches
### SW1
```
Switch>enable
Switch#configure terminal
SW1(config)#hostname SW1
SW1(config)#no ip domain-lookup
SW1(config)#enable secret cisco123
SW1(config)#service password-encryption
SW1(config)#line console 0
SW1(config)#password cisco
SW1(config)#login
SW1(config)#exit
```

### SW2
```
Switch>enable
Switch#configure terminal
Switch(config)#hostname SW2
SW2(config)#no ip domain-lookup
SW2(config)#enable secret cisco123
SW2(config)#service password-encryption
SW2(config)#line console 0
SW2(config)#password cisco
SW2(config)#login
SW2(config)#exit
```

### SW3
```
Switch>enable
Switch#configure terminal
Switch(config)#hostname SW3
SW3(config)#no ip domain-lookup
SW3(config)#enable secret cisco123
SW3(config)#service password-encryption
SW3(config)#line console 0
SW3(config)#password cisco
SW3(config)#login
SW3(config)#exit
```

## step 2: Create VLAN
### SW1
```
Switch>enable
Switch#configure terminal
SW1(config)#vlan 10
SW1(config-vlan)#name Student
SW1(config-vlan)#vlan 20
SW1(config-vlan)#name IT
SW1(config-vlan)#vlan 30
SW1(config-vlan)#name Teacher
end
```

### SW2
```
SW2(config)#vlan 10
SW2(config-vlan)#name Student
SW2(config-vlan)#vlan 20
SW2(config-vlan)#name IT
SW2(config-vlan)#vlan 30
SW2(config-vlan)#name Teacher
end
```
### SW3
```
SW3h#configure terminal
SW3(config)#vlan 10
SW3(config-vlan)#name Student
SW3(config-vlan)#vlan 20
SW3(config-vlan)#name IT
SW3(config-vlan)#vlan 30
SW3(config-vlan)#name Teacher
end
```
## Step 3: Assign VLAN to ports
### SW1

```
SW1(config)#interface fastEthernet0/1
SW1(config-if)##switchport mode access
SW1(config-if)#switchport access vlan 10
SW1(config-if)#exit

SW1(config)#interface fastEthernet0/2
SW1(config-if)#switchport mode access
SW1(config-if)#switchport access vlan 20
SW1(config-if)exit

SW1(config)#interface fastEthernet0/3
SW1(config-if)#switchport mode access
SW1(config-if)#switchport access vlan 30
SW1(config-if)exit
```

### SW3

```
SW3(config)#interface fastEthernet0/3
SW3(config-if)##switchport mode access
SW3(config-if)#switchport access vlan 10
SW3(config-if)#exit

SW3(config)#interface fastEthernet0/2
SW3(config-if)#switchport mode access
SW3(config-if)#switchport access vlan 20
SW3(config-if)exit

SW3(config)#interface fastEthernet0/1
SW3(config-if)#switchport mode access
SW3(config-if)#switchport access vlan 30
SW3(config-if)exit
```
## Step 4: Configure Trunk port
### SW1

```
SW1#configure terminal
SW1(config)#interface Giga0/1
SW1(config-if)#switchport mode trunk
SW1(config-if)#switchport trunk allowed vlan 10,20,30
```

### SW2

```
SW2#configure terminal
SW2(config)#interface Giga0/1
SW2(config-if)#switchport mode trunk
SW2(config-if)#switchport trunk allowed vlan 10,20,30
SW2(config-if)#exit

SW2#configure terminal
SW2(config)#interface Giga0/2
SW2(config-if)#switchport mode trunk
SW2(config-if)#switchport trunk allowed vlan 10,20,30
SW2(config-if)#exit
```
### SW3

```
SW3#configure terminal
SW3(config)#interface Giga0/1
SW3(config-if)#switchport mode trunk
SW3(config-if)#switchport trunk allowed vlan 10,20,30
SW3(config-if)#exit
```
