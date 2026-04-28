<img width="845" height="506" alt="image" src="https://github.com/user-attachments/assets/af553c85-3267-4f82-83dc-ddb4ef27fc10" />

---
## IP addresses

```bash
# ISP1
interface f0/0
	ip address 10.0.1.2 255.255.255.252
	no shutdown
	exit
interface f1/0
	ip address 11.0.9.1 255.255.255.252
	no shutdown
	exit
interface f2/0
	ip address 11.0.5.1 255.255.255.252
	no shutdown
	exit
interface f3/0
	ip address 11.0.6.1 255.255.255.252
	no shutdown
	exit
	
# ISP2
interface f0/0
	ip address 11.0.2.2 255.255.255.252
	no shutdown
	exit
interface f1/0
	ip address 11.0.5.2 255.255.255.252
	no shutdown
	exit
interface f2/0
	ip address 11.0.7.1 255.255.255.252
	no shutdown
	exit

# ISP3
interface f0/0
	ip address 11.0.3.2 255.255.255.252
	no shutdown
	exit
interface f1/0
	ip address 11.0.10.1 255.255.255.252
	no shutdown
	exit
interface f2/0
	ip address 11.0.8.1 255.255.255.252
	no shutdown
	exit
interface f3/0
	ip address 11.0.6.2 255.255.255.252
	no shutdown
	exit

# ISP4
interface f0/0
	ip address 11.0.4.2 255.255.255.252
	no shutdown
	exit
interface f1/0
	ip address 11.0.8.2 255.255.255.252
	no shutdown
	exit
interface f2/0
	ip address 11.0.7.2 255.255.255.252
	no shutdown
	exit
	
# on Edge-ISP
interface f0/0
	ip address 11.0.9.2 255.255.255.252
	no shutdown
	exit
interface f1/0
	ip address 11.0.10.2 255.255.255.252
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
	network 11.0.0.0 0.0.255.255 
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
<img width="681" height="675" alt="image" src="https://github.com/user-attachments/assets/c77f548d-9067-4044-97a9-f847e5c9c3b9" />

### ISP2
<img width="691" height="764" alt="image" src="https://github.com/user-attachments/assets/014e624d-c99b-4ede-b6c7-b575721235f0" />

### ISP3
<img width="717" height="671" alt="image" src="https://github.com/user-attachments/assets/fe9a853f-ef79-44cf-acc0-39d09a0b53f0" />

### ISP4
<img width="699" height="657" alt="image" src="https://github.com/user-attachments/assets/9533a533-bd0e-4318-a015-ae173bed3ee6" />

### Edge-ISP
<img width="692" height="686" alt="image" src="https://github.com/user-attachments/assets/a3a1cf4e-7bfd-4f1b-9079-92b865cb94eb" />

After we ping from a PC in siteA to the internet, the NAT translation happens on the Edge-ISP Router;
<img width="619" height="282" alt="image" src="https://github.com/user-attachments/assets/c7770f3e-3681-41df-8951-127ac85f18a6" />

