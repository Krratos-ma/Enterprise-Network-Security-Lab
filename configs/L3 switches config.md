![[Pasted image 20260112015520.png]]

---
## IP addresses

```bash
# on SW1 & SW2
int g1/0
	no switchport
	ip address 192.168.20.105 255.255.255.252
	no shut
```

---
## Etherchannel config

```bash
# on SW1 & SW2
int range g0/2-3
	shutdown
	no switchport
	channel-group 10 mode on
	no shutdown

# on SW1
int p10
	ip address 192.168.20.97 255.2555.255.252

# on SW2
int p10
	ip address 192.168.20.98 255.2555.255.252
```

---
## Trunk ports

```bash
# on SW1 & SW2
interface range g0/0-1 , g1/1
	switchport trunk encapsulation dot1q
	switchport mode trunk
```

---
## SVIs

run on SW1;
```bash
int vlan 10
	no sh
	ip add 192.168.20.30 255.255.255.224
int vlan 20
	no sh
	ip add 192.168.20.62 255.255.255.224
int vlan 30
	no sh
	ip add 192.168.20.94 255.255.255.224
```

run on SW2;
```bash
int vlan 10
	no sh
	ip add 192.168.20.29 255.255.255.224
int vlan 20
	no sh
	ip add 192.168.20.61 255.255.255.224
int vlan 30
	no sh
	ip add 192.168.20.93 255.255.255.224
```

---
## Standby

run on both SW1 and SW2;
```bash
int vlan 10
	standby 10 ip 192.168.20.20
	exit

int vlan 20
	standby 10 ip 192.168.20.50
	exit

int vlan 30
	standby 10 ip 192.168.20.80
	exit
```

---
## VTP

run this on SW1 to create the VTP domain;
```
vtp domain cisco123
```

and then on SW1
```
vlan 10
vlan 20
vlan 30
vlan 40
```

---
## OSPF

on SW1;
```bash
router ospf 1

## for G1/0
network 192.168.20.105 0.0.0.0 area 0 

## for SVIs
network 192.168.20.62 0.0.0.0 area 0
network 192.168.20.30 0.0.0.0 area 0
network 192.168.20.94 0.0.0.0 area 0
```

on SW2;
```bash
router ospf 1

## for G1/0
network 192.168.20.101 0.0.0.0 area 0 

## for SVIs
network 192.168.20.61 0.0.0.0 area 0
network 192.168.20.29 0.0.0.0 area 0
network 192.168.20.23 0.0.0.0 area 0
```

run on SW1 and SW2 to make **SVIs** passive interfaces;
```
router ospf 1
passive-interface vlan 10
passive-interface vlan 20
passive-interface vlan 30
```

---
## Show Commands

## On SW2
![[Pasted image 20260112034343.png]]

![[Pasted image 20260112034420.png]]

![[Pasted image 20260112034458.png]]

![[Pasted image 20260112034520.png]]

![[Pasted image 20260112034558.png#center]]

### On SW1
![[Pasted image 20260112034921.png]]

![[Pasted image 20260112034941.png#center]]