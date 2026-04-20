<img width="809" height="503" alt="Pasted image 20260112031749" src="https://github.com/user-attachments/assets/2bf011c4-adf1-4df2-993b-66827e733142" />

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
<img width="694" height="713" alt="Pasted image 20260112035929" src="https://github.com/user-attachments/assets/587d136b-393f-400c-ba4b-29ae9f67bf78" />

### ISP2
<img width="708" height="699" alt="Pasted image 20260112035529" src="https://github.com/user-attachments/assets/ac5b5276-afa6-450e-a92d-e16396307fdb" />

### ISP3
<img width="745" height="673" alt="Pasted image 20260112035719" src="https://github.com/user-attachments/assets/333f0927-1d62-4f6b-b210-83b20ff6cb46" />

### ISP4
<img width="717" height="653" alt="Pasted image 20260112035840" src="https://github.com/user-attachments/assets/69724189-83b4-40ff-9f8b-1530dc199dea" />

### Edge-ISP
<img width="689" height="554" alt="Pasted image 20260112040601" src="https://github.com/user-attachments/assets/1314568e-0266-4d6c-97b5-04601a0ab4bb" />

<img width="699" height="467" alt="Pasted image 20260112040658" src="https://github.com/user-attachments/assets/041cbd9f-b007-4fda-9b95-6e6bf973c840" />

