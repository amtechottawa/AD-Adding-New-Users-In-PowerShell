# Active Directory Adding A New User With Powershell
## Summary
This is a simple guide I created to make a new domain user in Active Directory  using PowerShell on Windows Server 2025, then verified the account and its profile details. 

## Environment 
-Hypervisor: VMware Workstation
-OS: Windows Server 2025
-Server: AM-DC-01 (Domain Controller)
-Domain: AM-Tech.local

##Steps

###1. Confirm user on powershell
PS C:\Users\Username> Get-Service

###2. Confirm the Domain
'''powershell
Get-ADDomain | Select DNSRoot, DistinguishedName
```
![Domain info](screenshot/1.png)

### 3. Create the User
'''powershell
-New-ADuser -Name "Kenna Earl" '
-GivenName "Kenna" -Surname "Earl" '
-SamAccount "kearl" '
-UserPrincipalName "kearl@AMTech.local" '
-Title "Help Desk Support" ' 
-Department "IT" '
-Path "CN=Users, DC=AMTech, DC=local" '
-AccountPassword (ReadHost -AsSecureString "Enter password") '
-ChangePasswordAtLogon $true '
-Enable $true
```
![Creating the user] (screenshots/2.png)

###4. Confirm in Active Directory Users and Computers
![User in ADUC] (screenshot/4.png)




