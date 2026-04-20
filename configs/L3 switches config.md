<img width="855" height="393" alt="Pasted image 20260112015520" src="https://github.com/user-attachments/assets/db64937e-ef7f-4f9a-98eb-2667379b5fa0" />

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
<img width="654" height="423" alt="Pasted image 20260112034343" src="https://github.com/user-attachments/assets/c051bc56-e0d0-4e23-8390-ab232058b4d5" />

<img width="659" height="443" alt="Pasted image 20260112034420" src="https://github.com/user-attachments/assets/d805e3af-736c-448d-b260-169d1d0d06ad" />

<img width="654" height="585" alt="Pasted image 20260112034458" src="https://github.com/user-attachments/assets/95b2158e-8921-4651-9521-79f053ce5a8b" />

<img width="697" height="59" alt="Pasted image 20260112034520" src="https://github.com/user-attachments/assets/cb3be0c7-4b11-415d-b5e7-f5e75342a463" />

<img width="365" height="149" alt="Pasted image 20260112034558" src="https://github.com/user-attachments/assets/c26c2f8b-2079-4d48-a513-fdd28cc51b24" />

### On SW1
<img width="654" height="605" alt="Pasted image 20260112034921" src="https://github.com/user-attachments/assets/264d2645-b8b0-4774-8347-39f5fce0597f" />

<img width="806" height="630" alt="Pasted image 20260112034941" src="https://github.com/user-attachments/assets/430b3d2c-dff9-4f0f-a67e-58775a69947f" />
