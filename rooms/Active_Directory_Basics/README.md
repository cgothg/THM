# Notes for the room "Active Directory Basics"

## Tasks:

### Task 2

What database does the AD DS contain?

```
NTDS.dit
```

Where is the NTDS.dit stored?

```
%SystemRoot%\NTDS
```

What type of machine can be a domain controller?

```
Windows server
```

### Task 3

What is the term for a hierarchy of domains in a network?

```
Tree
```

What is the term for the rules for object creation?

```
Domain Schema
```

What is the term for containers for groups, computers, users, printers, and other OUs?

```
Organizational Units
```

### Task 4

Which type of groups specify user permissions?

```
Security Groups
```

Which group contains all workstations and servers joined to the domain?

```
Domain Computers
```

Which group can publish certificates to the directory?

```
Cert Publishers
```

Which user can make changes to a local machine but not to a domain controller?

```
Local Administrators
```

Which group has their passwords replicated to read-only domain controllers?

```
Allowed RODC Password Replication Group
```

### Task 5


What type of trust flows from a trusting domain to a trusted domain?

```
Directional
```

What type of trusts expands to include other trusted domains?

```
Transitive
```

### Task 6

What type of authentication uses tickets?

```
Kerberos
```

What domain service can create, validate, and revoke public key certificates?

```
Certificate Services
```

### Task 7

What is the Azure AD equivalent of LDAP?

```
Rest APIs
```

What is the Azure AD equivalent of Domains and Forests?

```
Tenants
```

What is the Windows Server AD equivalent of Guests?

```
Trusts
```

### Task 8

What is the name of the Windows 10 operating system?

```
Windows 10 Enterprise Evaluation
```

What is the second "Admin" name?

```
Admin2
```

Which group has a capital "V" in the group name?

Used the command: `Get-NetGroup -GroupName *`

```
Hyper-V Administrators
```

When was the password last set for the SQLService user?

Used this command: `Get-NetUser -SPN | ?{$_.memberof -match 'Domain Admins'}`

```
5/14/2020 3:42:53 AM
```
