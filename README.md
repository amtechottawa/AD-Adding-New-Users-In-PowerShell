# Adding a New User with PowerShell in Active Directory

## Summary

This is a simple guide I created to make a new domain user in Active Directory using PowerShell on Windows Server 2025. I used VMware Workstation to test it.

## Environment

- Hypervisor: VMware Workstation
- OS: Windows Server 2025
- Server: AM-DC-01 (Domain Controller)
- Domain: AM-Tech.local

## Steps

### 1. Confirm PowerShell

```powershell
Get-Service
```

<div align="center">
  <img src="https://github.com/user-attachments/assets/6ce3e7d0-572d-4e2c-a9e3-c5322d3a8395" alt="Verify on PowerShell" width="80%">
</div>

### 2. Confirm the Domain

```powershell
Get-ADDomain | Select-Object DNSRoot, DistinguishedName
```

<div align="center">
  <img src="https://github.com/user-attachments/assets/4d362abb-c749-41f4-b8ee-44b5bf6c7556" alt="Domain Confirmation" width="80%">
</div>

### 3. Create the User

```powershell
New-ADUser -Name 'Kenna Earl' -GivenName 'Kenna' -Surname 'Earl' -SamAccountName 'kearl' -UserPrincipalName 'kearl@AM-Tech.local' -Title 'Help Desk Support' -Department 'IT' -Path 'CN=Users,DC=AM-Tech,DC=local' -AccountPassword (Read-Host -AsSecureString 'Enter password') -ChangePasswordAtLogon $true -Enabled $true
```

<div align="center">
  <img src="YOUR-IMAGE-URL-HERE" alt="User Creation" width="80%">
</div>

### 4. Verify the Account

```powershell
Get-ADUser kearl -Properties Title, Department, Enabled | Select-Object Name, SamAccountName, Title, Department, Enabled
```

<div align="center">
  <img src="https://github.com/user-attachments/assets/a8a29939-6c32-4ec6-b629-e21e5e8f2c95" alt="User Creation Verification" width="80%">
</div>

## Little Note on Security

- `ChangePasswordAtLogon` would normally be set to `$false` if the user should keep the temporary password. I chose to set it to `$true` so that Windows requires the user to create a new password when they first log in.

- The password could be more complex, but since this is a simple lab, the default password requirements are being used.

## What I Learned

- GitHub Markdown syntax and basic PowerShell commands using Windows Server 2025.
- Setting up a new user through the GUI produces the same result, but PowerShell is faster.
- Verifying user accounts with `Get-ADUser`.
- Passwords should never be hard-coded into scripts.
