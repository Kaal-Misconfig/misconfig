+++
title = "Active Directory Groups"
summary = "Read more.."
date = "2025-11-21"
tags = ["Active Directory"]
categories = ["Notes"]
+++

##### **Groups** in AD are used to group users together so you can assign them access rights all at once (like access to a file server or printer). They're powerful, but if not managed well, they can accidentally give too much access, which attackers love to abuse. Companies often have both built-in and custom groups. Overtime, too many groups can cause confusion and lead to unintended access, so it's important to regularly audit group memberships and permissions.

### <span style="color:rgb(68, 255, 0)">Difference Between Groups and OUs</span> 
- **Groups**: Used to assign permissions
- **OUs**: Used to organize and manage users, computers and groups. You can apply policies or delegate control without giving full admin rights.


## Types of <span style="color:rgb(68, 255, 0)">Groups</span> 

##### Groups in AD have two fundamental characteristics: <span style="color:rgb(69, 236, 9)">type</span> and <span style="color:rgb(69, 236, 9)">scope</span>. the group type defines the groups's purpose, while the group scope shows how the group can be used within the domain or forest.

## Group <span style="color:rgb(126, 226, 44)">Types</span>

### <span style="color:rgb(134, 255, 36)">Security Groups </span>
-> The security groups type is primarily for ease of assigning permissions and rights to a collection of users instead of one at a time. They simplify management and reduce overhead when assigning permissions and rights for a given resource. All users added to a security group will inherit any permissions assigned to the group, making it easier to move users in and out of groups while leaving the group's permissions unchanged.

### <span style="color:rgb(126, 226, 44)">Distribution Groups</span> 
-> The distribution groups type is used by email applications such as Microsoft Exchange to distribute messages to group members. they function much like mailing lists and allow for auto-adding emails in the "To" field when creating an email in Microsoft Outlook. this type of group cannot be used to assign permission to resources in a Domain environment.


## Group <span style="color:rgb(126, 226, 44)">Scopes</span> 

### <span style="color:rgb(126, 226, 44)">Domain Local Groups</span> 
-> Domain Local groups can only be used to manage permissions to domain resources in the domain where it was created. Local Groups cannot be used in other domains but CAN contain users from other domains. Local groups can be nested into other local groups but not within global groups.

### <span style="color:rgb(126, 226, 44)">Global Group
</span> 
-> Global groups can be used to grant access to resources in another domain. A global group can only contain accounts from the domain where it was created. Global groups can be added to both other global groups and local groups.


### <span style="color:rgb(126, 226, 44)">Universal Group</span> 
-> Universal groups in AD are used when you need to manage access across multiple domains in the same forest. They can include from users any domain and give access to any resource in the forest.
This groups are stored in GC (Global Catalog), so changes to them causes forest-wide replication, meaning the update gets sent to all domains.

#### <span style="color:rgb(125, 125, 125)">Example</span> 
```PowerShell
Get-ADGroup -Filter * | select samaccountname, groupscope

samaccountname                           groupscope
--------------                           ----------
Administrators                          DomainLocal
Users                                   DomainLocal
Guests                                  DomainLocal
Print Operators                         DomainLocal
Backup Operators                        DomainLocal
Replicator                              DomainLocal
Remote Desktop Users                    DomainLocal
Network Configuration Operators         DomainLocal
Distributed COM Users                   DomainLocal
IIS_IUSRS                               DomainLocal
Cryptographic Operators                 DomainLocal
Event Log Readers                       DomainLocal
Certificate Service DCOM Access         DomainLocal
RDS Remote Access Servers               DomainLocal
RDS Endpoint Servers                    DomainLocal
RDS Management Servers                  DomainLocal
Hyper-V Administrators                  DomainLocal
Access Control Assistance Operators     DomainLocal
Remote Management Users                 DomainLocal
Storage Replica Administrators          DomainLocal
Domain Computers                             Global
Domain Controllers                           Global
Schema Admins                             Universal
Enterprise Admins                         Universal
Cert Publishers                         DomainLocal
Domain Admins                                Global
Domain Users                                 Global
Domain Guests                                Global
```

#### <span style="color:rgb(255, 255, 0)">NOTE</span> 
- A Global  Group can only be converted into Universal Group if it is NOT part of another Global Group
- A Domain Local Group can only be converted to a Universal Group if the Domain Local Group does NOT contain any other domain local groups as members.
- A universal group can be converted to a Domain Local Group without any restrictions.
- A Universal Group can only be converted to a Global Group if it does NOT contain any other Universal Groups as Members


# <span style="color:rgb(255, 255, 0)">Built-In Vs Custom Groups</span> 

##### When a new domain is created in AD, several built-in security groups are automatically made. These groups usually have a Domain Local scope and are used for specific admin tasks. You can't nest groups inside these built-in ones, only user accounts can be added.
##### Organizations usually create their own custom groups and new services like Microsoft Exchange can also automatically add new privileged groups to AD. If these aren't reviewed and managed properly, attackers can use them to gain high-level access.



# <span style="color:rgb(126, 226, 44)">Nested</span> Group Membership

##### In AD, Groups can be nested, So if User A is in Group 1, and Group 1 is in Group 2, User A gets the permissions of Group 2, even if not directly added to it. Nested groups can unintentionally give away powerful access. **Use BloodHound to visualize and detect these hidden paths**, it’s crucial for both **pentesters** and **sysadmins**.


# <span style="color:rgb(255, 64, 0)">Important</span> Group <span style="color:rgb(126, 226, 44)">Attributes</span> 

1. **cn**: Common-Name is the name of the group in AD DS.
2. **member**: Which user, group and contact objects are member of the group.
3. **groupType**: An integer that specifies the group type and scope
4. **memberOf**: A listing of any groups that contain the group as a member.
5. **objectSID**: This is the security identifier or SID of the group, which is the unique value used to identify the group as a security principal.

