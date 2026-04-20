![[Pasted image 20260112043208.png]]
# Installing Windows server 2016
## Downloading the ISO image from the web
- go to https://www.microsoft.com/en-us/evalcenter/download-windows-server-2016
- Choose the **ISO dowloand** from the English(United states) bar.
- wait till it's done downloading.
- follow steps in the section  "**Install any VM in EVE-NG to set up the VM**"
--- 
## Start and set up your machine inside Virtual box
- start your machine > keep the default settings and keep clicking next till you get here;
![[Pasted image 20250921090438.png|400]]
- choose **Windows Server 2025 Standard Evaluation (Desktop Eperience)**.

- keep clicking next and choose your keyboard layout and stuff. 
- wait for this and choose to reboot the machine once it ends;
![[Pasted image 20250921090618.png|300]]

- keep choosing typical settings, enter your administrator password. ^res1
--- 
# Configuring Server as a Domain Controller

## Changing PC name to DC01 ^res1
- once logged in to your admin account in the windows 2025 server. Go to start menu and type "view my pc name" > once in settings, choose rename this PC > give it the name "DC01" and let it restart > click next to keep defaullt choice.
--- 
## Adding the Active Directory Domain Services role
- then, you'll go to the server manager dashboard that pops up to you > go here;
![[Pasted image 20250921093841.png]]

- keep default settings and keep clicking next till you get to the **server roles** panel on the left and choose "Active Directory Domain Services" > click add features, and keep hiting next till you get here and check this;
![[Pasted image 20250921095210.png]]
- hit **Next**

- and install at the end.

- wait this till it's done and then click here;
![[Pasted image 20250921094117.png|400]]

![[Pasted image 20250921094229.png|400]]
- then hit **Next**
- "LAB.local" can be anything you want, (e.g. company.com).

- keep all settings as default in next page that would pop up, just enter a password for the domain. 
![[Pasted image 20250921094456.png|400]]

- keep clicking next and keep default settings and click Install at last step and let it reboot itself.
--- 
## Adding the Active Directory Certificate Services role
- add another role 
![[Pasted image 20250921093841.png]]

- keep default settings again till you get to server roles and choose "Active Directory Certificate Services" > then click **Add features** in the window that pops up.
- And keep clicking next with default settings till you get here again and check this again;
![[Pasted image 20250921095210.png|400]]

- click Install at the end again till it's done and click here;
![[Pasted image 20250921095617.png|400]]
- click next and keep default settings 

- once you get here, check this;
![[Pasted image 20250921095749.png|400]]

- keep clicking **Next** and click **Configure** at the end. Once it's done, close all windows.
- now we're done setting up this server as a domain controller and we created a domain called "LAB.local" in it.
---
# Attaching Windows 11 VM to Domain
## change network settings on Windows 2016 server VM 
- go into the Windows 2016 server VM
- login to the admin account
- set up a static IP from control panel > Network > network and sharing center >  change adapetr settings from left panel -> click the NIC and go to TCP/IPv4 >  give a static IP, subnet mask and default gateway and set the DNS to "127.0.0.1" to refer back to current machine, because we'll use the windows server 2025 machine as the DNS server.
- click OK > click OK 
--- 
## changing the windows 10 VM in Sales or HR VLAN
- from the windows 10 VM, Go to start menu and type "view my pc name" > once in settings, choose rename this PC > give it the name Sales1 or HR1 or HR3 pr Sales3 depends on which VM in the lab you're using and let it restart > click next to keep defaullt choice.
- after setting UP all windows machines to join the AD, we can check that all workstations are added here;
![[Pasted image 20260112042814.png]]
--- 
## attach the Windows 10 VM to our domain and login to the admin account
- go the Windows 10 VM
- type "access work or school" in start menu
- click "connect" on the top
- enter the domain name (e.g. "LAB.local") 
- enter the domain's admin password.
- keep default settings and hit **Next**.
- click **Restart now**
- once on login page, choose **Other User** from bottom left > enter username and password of one of the users created earlier here;
![[Pasted image 20260112042735.png]]
- done.
--- 
## Purpose of the note
- in this note, we'll see how to set the account for an AD user to be locked after a specific number of attempts entering a wrong password.

--- 
## Add the [[Group Policy Objects]] that locks the account after a number of failing attempts to the domain
- go to the domain controller machine server dashboard > **tools** on top right > **Group Policy Objects** > right click the domain "LAB.local" > **create GPO and link it here**(1st option) > give the GPO a name "AccountLockoutPolicy" > 

- then right click the GPO from left panel > choose **Edit**.
![[Pasted image 20250924173747.png]]


- navigate to **Policies** > **Windows Settings** > **Security Settings** > **Account Plicies** > **Account Lockout** > double click on "Account lockout threshold"
![[Pasted image 20250924173924.png]]

- check "**Define this Policy Setting**" > enter the number of failed attempts that would lead to the account being locked (e.g. "3")
- click **Apply** > **OK** > **OK**. 
- some other settings will be adjusted automatically like "Account lockout duration" which will be set to a suggested number like "10 minutes" which means the account will be locked for 10 minutes before the user can try to enter the password again.

---
## What can you do to check the GPO works?
- now, you can login from a remote WS with an AD user and try to enter wrong password more than 3 times like we set before > you'll get a prompt telling you the account is locked, after that, the account will be locked for 10 minutes as we set before

--- 
## Resetting the AD user password to unlock their account
- if you wanna unlock the account again before this duration, go to the server dashboard > **tools** from top right > **Active Directory Users and Computers** > click here;
![[Pasted image 20250924172922.png]]
- then enter the username and click **Find Now** from the right.
- this will enable you to find the user easily.
- then right click on the user > choose **reset password** > and enter the new password
- you can check "**user must change password at next logon**"

- however, if you can't check it, cancel and double click the user > go to the **Account** tab and from the list in the middle > uncheck "**password never expires**" if checked > and click **Apply** > and **OK**.
- and then try to reset the password again and you'll be able to check the "**user must change password at next logon**" line when resetting the password.

- like that, the AD user will be able to login remotely using the new password you set and will be prompted to enter their new password afterwards.
---

