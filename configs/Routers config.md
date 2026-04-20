![[Pasted image 20260112031749.png]]

---
## IP addresses

```bash
# ISP1
interface f0/0
	ip address 10.0.1.2 255.255.255.252
	no shutdown
	exit
interface f1/0
	ip address 10.0.9.1 255.255.255.252
	no shutdown
	exit
interface f2/0
	ip address 10.0.5.1 255.255.255.252
	no shutdown
	exit
interface f3/0
	ip address 10.0.6.1 255.255.255.252
	no shutdown
	exit
	
# ISP2
interface f0/0
	ip address 10.0.2.2 255.255.255.252
	no shutdown
	exit
interface f1/0
	ip address 10.0.5.2 255.255.255.252
	no shutdown
	exit
interface f2/0
	ip address 10.0.7.1 255.255.255.252
	no shutdown
	exit

# ISP3
interface f0/0
	ip address 10.0.3.2 255.255.255.252
	no shutdown
	exit
interface f1/0
	ip address 10.0.10.1 255.255.255.252
	no shutdown
	exit
interface f2/0
	ip address 10.0.8.1 255.255.255.252
	no shutdown
	exit
interface f3/0
	ip address 10.0.6.2 255.255.255.252
	no shutdown
	exit

# ISP4
interface f0/0
	ip address 10.0.4.2 255.255.255.252
	no shutdown
	exit
interface f1/0
	ip address 10.0.8.2 255.255.255.252
	no shutdown
	exit
interface f2/0
	ip address 10.0.7.2 255.255.255.252
	no shutdown
	exit
	
# on Edge-ISP
interface f0/0
	ip address 10.0.9.2 255.255.255.252
	no shutdown
	exit
interface f1/0
	ip address 10.0.10.2 255.255.255.252
	no shutdown
	exit
interface f2/0
	ip address dhcp
	no shutdown
	exit
```

----
## OSPF

```bash
# on ALL routers
router ospf 1
	network 10.0.0.0 0.0.255.255 
```

----
## Default Route to internet

```bash
# on Edge-ISP
router ospf 1
	default-information originate
```

---
## PAT (NAT overload) on Edge-ISP

```bash
access-list 10 permit any
ip nat inside source list 10 interface f2/0 overload

interface f0/0 
ip nat inside

interface f1/0
ip nat inside

interface f2/0
ip nat outside 
```

---
## Show commands

### ISP1
![[Pasted image 20260112035929.png]]

### ISP2
![[Pasted image 20260112035529.png]]

### ISP3
![[Pasted image 20260112035719.png]]

### ISP4
![[Pasted image 20260112035840.png]]

### Edge-ISP
![[Pasted image 20260112040601.png]]

![[Pasted image 20260112040658.png]]

