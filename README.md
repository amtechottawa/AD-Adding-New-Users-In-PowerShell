# Active Directory Adding A New User With Powershell via VMware 2025
## Summary
This is a simple guide I created to make a new domain user in Active Directory  using PowerShell on Windows Server 2025, then verified the account and its profile details. 

## Environment 
-Hypervisor: VMware Workstation
-OS: Windows Server 2025
-Server: AM-DC-01 (Domain Controller)
-Domain: AM-Tech.local

##Steps

### 1. Confirm user on powershell
```powershell
'PS C:\Users\Username> Get-Service'
```
![Verify on Powershell](screenshot/1.png)

### 2. Confirm the Domain

```powershell
Get-ADDomain | Select Object DNSRoot, DistinguishedName
```

![Domain info](screenshot/2.png)

### 3. Create the User

```powershell
New-AdUser -Name 'Kenna Earl' `
           -GivenName 'Kenna' `
           -Surname 'Earl' `
           -SameAccountName 'kearl' `
           -UserPrincipalName 'kearl@AMTech.local' `
           -Title 'Help Desk Support' `
           -Department 'IT' `
           -Path 'CN-Users, DC=AMTech, DC=local' `
           -AccountPassword (Read-Host -AsSecureaString 'Enter password')
           -ChangePasswordAtLogon $true `
           -Enabled \$true

```
![Active Directory User Created Successfully](screenshot/3.png)

### 4 Verify The Account
```powershell
Get-AddUser kearl -Properties Title, Department, Enabled | Select Name, SamAccountName, Title, Department, Enabled
```
![Verification of account](screenshots/4.png)
           
##Little Note on Security
-ChangePasswordAtLogon would normally be set to false so the user could use the temperary password but I chose to change it to true so that when they log in they windows will enact a new password increasing security posture
-The password could be more complex but since this is a simple lab, the default password standards will be in place

##What I learned
-Github syntax and powershell basic commands via Windows Server 2025
-Setting up a new user via the gui will result in the same but powershell is faster
-Verifying the accounts with 'Get-AdUser'
-Passwords should never be coded into the scripts







