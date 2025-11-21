+++
title = "Active Directory Rights and Privileges"
summary = "Read more.."
+++

##### <span style="color:rgb(126, 226, 44)">Rights</span> are typically assigned to users or groups and deal with permissions to access an object such as file, while <span style="color:rgb(126, 226, 44)">privileges</span> grant a user permission to perform an action such as run a program, shut down a system, reset passwords, etc. Privileges can be assigned individually to users or conferred upon them via built-in or custom group membership.  

### Server <span style="color:rgb(126, 226, 44)">Operators</span>

```PowerShell
Get-ADGroup -identity "Server Operators" -Properties *

adminCount                      : 1
CanonicalName                   : INLANEFREIGHT.LOCAL/Builtin/Server Operators
CN                              : Server Operators
Created                         : 10/27/2021 8:14:34 AM
createTimeStamp                 : 10/27/2021 8:14:34 AM
Deleted                         : 
Description                     : Members can administer domain servers
DisplayName                     : 
DistinguishedName               : CN=Server Operators,CN=Builtin,DC=INLANEFREIGHT,DC=LOCAL
dSCorePropagationData           : {10/28/2021 1:47:52 PM, 10/28/2021 1:44:12 PM, 10/28/2021 1:44:11 PM, 10/27/2021 
                                  8:50:25 AM...}
GroupCategory                   : Security
GroupScope                      : DomainLocal
groupType                       : -2147483643
HomePage                        : 
instanceType                    : 4
isCriticalSystemObject          : True
isDeleted                       : 
LastKnownParent                 : 
ManagedBy                       : 
MemberOf                        : {}
Members                         : {}
Modified                        : 10/28/2021 1:47:52 PM
modifyTimeStamp                 : 10/28/2021 1:47:52 PM
Name                            : Server Operators
nTSecurityDescriptor            : System.DirectoryServices.ActiveDirectorySecurity
ObjectCategory                  : CN=Group,CN=Schema,CN=Configuration,DC=INLANEFREIGHT,DC=LOCAL
ObjectClass                     : group
ObjectGUID                      : 0887487b-7b07-4d85-82aa-40d25526ec17
objectSid                       : S-1-5-32-549
ProtectedFromAccidentalDeletion : False
SamAccountName                  : Server Operators
sAMAccountType                  : 536870912
sDRightsEffective               : 0
SID                             : S-1-5-32-549
SIDHistory                      : {}
systemFlags                     : -1946157056
uSNChanged                      : 228556
uSNCreated                      : 12360
whenChanged                     : 10/28/2021 1:47:52 PM
whenCreated                     : 10/27/2021 8:14:34 AM
```


### Domain <span style="color:rgb(255, 64, 0)">Admins</span>

```PowerShell
Get-ADGroup -identity "Domain Admins" -properties * | select DistinguishedName, GroupCategory, GroupScope, Name, Members


DistinguishedName : CN=Domain Admins,CN=Users,DC=INLANEFREIGHT,DC=LOCAL
GroupCategory     : Security
GroupScope        : Global
Name              : Domain Admins
Members           : {CN=htb-student_adm,CN=Users,DC=INLANEFREIGHT,DC=LOCAL, CN=sharepoint admin,CN=Users,DC=INLANEFREIGHT,DC=LOCAL, CN=FREIGHTLOGISTICSUSER,OU=Service Accounts,OU=Corp,DC=INLANEFREIGHT,DC=LOCAL, CN=PROXYAGENT,OU=Service Accounts,OU=Corp,DC=INLANEFREIGHT,DC=LOCAL...}

```



# User Rights <span style="color:rgb(126, 226, 44)">Assignement</span> 

##### Depending on their current group membership, and other factors such as privileges that administrators can assign via Group Policy (GPO), users can have various rights assigned to their account. Some rights granted to an account can lead to unintended consequences such as privilege escalation or access to sensitive files. we could potentially leverage a tool such as [SharpGPOAbuse](https://github.com/FSecureLABS/SharpGPOAbuse) to assign targeted rights to a user.

 
1. **SeRemoteInteractiveLogonRight**: This privilege could give our target user the right to log onto a host via Remote Desktop, which could potentially be used to obtain sensitive data or escalate privileges. 
2. **SeBackupPrivilege**: This grants a user the ability to create system backups and could be used to obtain copies of sensitive system files that can be used to retrieve passwords such as the SAM and SYSTEM Registry hives and the NTDS.dit AD database file.
3. **SeDebugPrivilege**: This allows a user to debug and adjust the memory of a process. With this privilege, attackers could utilize a tool such as Mimikatz to read the memory space of the Local System Authority (LSASS) process and obtain any credentials stored in memeory.
4. **SeImpersonatePrivilege**: This privilege allows us to impersonate a token of a privileged account such as <span style="color:rgb(163, 254, 88)">NT AUTHORITY\SYSTEM</span>. This could be leveraged with a tool such as JuicyPotato, RogueWinRM, PrintSpoofer, to escalate privileges on a target system.
5. **SeLoadDriverPrivilege**: A user with this privilege can load and unload device drivers that could potentially be used to escalate privileges or compromise a system.
6. **SeTakeOwnershipPrivilege**: This allows a process to take ownership of an object. At its most basic level, we could use this privilege to gain access to a file share on a share that was otherwise not accessible to us.
