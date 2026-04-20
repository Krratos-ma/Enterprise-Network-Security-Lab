<img width="858" height="480" alt="Pasted image 20260112015029" src="https://github.com/user-attachments/assets/076295ad-d786-451f-9169-446db9943a7e" />

---
## Access ports
```bash
# on Access-Switch1
interface range e0/0 - e0/2
	switchport mode access
	switchport access vlan 20
	
# on Access-Switch2
interface range e1/2 , e0/1 , e1/1
	switchport mode access
	switchport access vlan 10

# on Access-Switch3
interface range e0/2 , e0/3 , e1/1
	switchport mode access
	switchport access vlan 30
```

---
## Access ports
```bash
# on Access-Switch1 & Access-Switch2
interface range e1/0 , e0/3
switchport trunk encapsulation dot1q
switchport mode trunk

# on Access-Switch3
interface range e0/0 , e0/1
switchport trunk encapsulation dot1q
switchport mode trunk
```

---
## Show commands

### On Access-Switch1
<img width="663" height="328" alt="Pasted image 20260112033340" src="https://github.com/user-attachments/assets/07191d08-e656-4ca7-a751-78bb463a3396" />

<img width="668" height="389" alt="Pasted image 20260112033608" src="https://github.com/user-attachments/assets/b889bf32-04cc-45a1-ad99-d65fc03d4191" />


<img width="666" height="461" alt="Pasted image 20260112034036" src="https://github.com/user-attachments/assets/a7f35f01-15b7-4e44-b636-bbd2a4c81872" />

### On Access-Switch2
<img width="665" height="435" alt="Pasted image 20260112033737" src="https://github.com/user-attachments/assets/485088e1-ffe1-4e95-87cc-4c855296539f" />


<img width="668" height="440" alt="Pasted image 20260112033807" src="https://github.com/user-attachments/assets/f1797975-f471-4d48-92f2-6b18a19df1b1" />

<img width="661" height="467" alt="Pasted image 20260112034109" src="https://github.com/user-attachments/assets/2be8b1ad-2d88-4e8c-8758-1e588e99b24b" />

### On Access-Switch3
<img width="661" height="467" alt="Pasted image 20260112034109" src="https://github.com/user-attachments/assets/63e9b4e3-97ba-4175-83a1-58db2e04184d" />

<img width="665" height="363" alt="Pasted image 20260112034135" src="https://github.com/user-attachments/assets/d6c7739f-17cd-47e6-b042-b9ede71b4056" />

<img width="652" height="383" alt="Pasted image 20260112034219" src="https://github.com/user-attachments/assets/1b7c0b07-8085-48f9-bb56-405c01fdb980" />


## Pinging The internet
<img width="660" height="419" alt="Pasted image 20260112041057" src="https://github.com/user-attachments/assets/1d0fe2c5-17a8-4b38-b159-7981cc35dc5a" />

- ``8.8.8.8`` isn't a loopback IP address, we're directly pinging the DNS public IP address from an endhost in VLAN10 in siteA
