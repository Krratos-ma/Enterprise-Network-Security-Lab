![[Pasted image 20260112021338.png#center]]

---
## MGMT Interface from CLI

```
configure
set deviceconfig system type static
set deviceconfig system ip-address 10.10.10.2 netmask 255.255.255.252
commit
exit
```
---
## Interfaces
![[Pasted image 20260112021723.png]]

---
## Tunnel Interface
![[Pasted image 20260112030214.png]]
## Zones
![[Pasted image 20260112021748.png#center]]
## Virtual router
![[Pasted image 20260112021839.png]]
### Default & VPN routes
![[Pasted image 20260112022314.png]]

![[Pasted image 20260112022001.png#center]]

![[Pasted image 20260112022422.png#center]]
## IPsec VPN

### IKE Profile
![[Pasted image 20260112022708.png]]
### IPsec Profile
![[Pasted image 20260112022739.png]]

<div style="text-align: center;">
<h3>IKE Gateway</h3>
</div>
![[Pasted image 20260112022804.png#center]]
### IPsec Tunnel
![[Pasted image 20260112025958.png]]
## Policies
![[Pasted image 20260112030111.png]]
## OSPF
![[Pasted image 20260112030700.png]]
### OSPF Neighbors 
![[Pasted image 20260112030719.png]]

### Passive interfaces
![[Pasted image 20260112031312.png]]

![[Pasted image 20260112031342.png]]

---
## Mgmt interface
![[Pasted image 20260112044900.png]]

## VPN show from CLI
![[Pasted image 20260112045133.png]]