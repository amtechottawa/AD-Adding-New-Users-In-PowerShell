# Using Adding A New User With Powershell On Active Directory
## Summary
This is a simple guide I created to make a new domain user in Active Directory using PowerShell on Windows Server 2025. This is VMware to test it out.

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
<div align="center">
  <figure>
    <img src="https://githubusercontent.com" alt="Verify on PowerShell" width="80%">
    <figcaption style="margin-top: 10px; color: #8b949e;"><em><img width="992" height="623" alt="1" src="https://github.com/user-attachments/assets/6ce3e7d0-572d-4e2c-a9e3-c5322d3a8395"/>
</em></figcaption>
  </figure>
</div>



### 2. Confirm the Domain

```powershell
Get-ADDomain | Select Object DNSRoot, DistinguishedName
```
<div align="center">
  <figure>
    <img src="https://githubusercontent.com" alt="Domain Confirmation" width="80%">
    <figcaption style="margin-top: 10px; color: #8b949e;"><em><img width="994" height="627" alt="2" src="https://github.com/user-attachments/assets/4d362abb-c749-41f4-b8ee-44b5bf6c7556" />

  </figure>
</div>

### 3. Create the User

```powershell
New-AdUser -Name 'Kenna Earl' -GivenName 'Kenna' -Surname 'Earl' -SamAccountName 'kearl' -UserPrincipalName 'kearl@AMTech.local' -Title 'Help Desk Support' -Department 'IT' -Path 'CN=Users,DC=AMTech,DC=local' -AccountPassword (Read-Host -AsSecureString 'Enter password') -ChangePasswordAtLogon true -Enabled true
```

![Active Directory User Created Successfully](<img width="1026" height="659" alt="image" src="https://github.com/user-attachments/assets/bedc3528-66c5-4432-a309-1c4a177544fc" />)



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







