+++
title = "Active Directory Objects"
summary = "Read more.."
+++
#### <span style="color:rgb(68, 255, 0)">Users</span> 
-> A user in AD is a digital account for a person that allows them to log in and access resources on the network. It's a leaf object, meaning it can't contain any other objects and it has SID and GUID. Each user can have 100s of attributes, like name, email, last login time...

#### <span style="color:rgb(68, 255, 0)">Contacts</span> 
-> A contact object is usually used to represent an external user and contains informational attributes such as first name, last name email address, etc, They are leaf objects and not security principals, they don't have SID only have a GUID.

#### <span style="color:rgb(68, 255, 0)">Printers</span> 
-> A printer objects points to printer accessible within AD network. Like a contact, a printer is a leaf object and not a security principal, so it only has a GUID 

#### <span style="color:rgb(68, 255, 0)">Computers</span>
-> A computer object is any computer joined to AD network. Computers are leaf objects and they are security principals means they have SID and GUID

#### <span style="color:rgb(68, 255, 0)">Shared Folders</span> 
-> Shared Folder object points to a shared folder on the specific computer where the folder resides. Shared Folder can have stringent access control applied to them and can be either accessible to everyone, even those without a valid AD account, open to only authenticated users , They are not security principals and only have a GUID

#### <span style="color:rgb(68, 255, 0)">Groups</span> 
-> Group is considered a container object because it can contain other objects, including users, computers, and even other groups. A group is regarded as a security principal and has a SID and a GUID. In AD,  groups are a way to manage user permissions and access to other securable objects.Common attributes are name, description, membership and other groups that the group belongs to.

#### <span style="color:rgb(68, 255, 0)">Organizational Units</span> 
-> OU is a container that systems administrators can use to store similar objects for ease of administration. OUs are often used for administrative delegation of tasks without granting a user account full rights. OUs are very useful for managing Group Policy links, and performing password resets.

#### <span style="color:rgb(68, 255, 0)">Domain</span> 
-> A domain is a the structure of an AD network. Domains contain objects such as users and computers, which are organized into container objects: groups and OUs. Every domain has its own separate database and sets of policies that can be applied to any and all objects within a domain.

#### <span style="color:rgb(68, 255, 0)">Domain Controller</span> 
-> Domain Controllers are essentially the brains of an AD network. They handle authentication requests, verify users on the network, and control who can access the various resources in the domain. All access requests are validated via the DC and privileged access requests are based on predetermined roles assigned to users. It also enforces security policies ans stores information about every other object in the domain.

#### <span style="color:rgb(68, 255, 0)">Sites</span> 
-> A site in AD is a set of computers across one or more subnets connected using high speed links. They are used to make replication across domain controllers run efficiently.

#### <span style="color:rgb(68, 255, 0)">Built-in
</span> 
-> In AD, Built-in is a container that holds default groups in an AD domain. They are predefined when an AD domain is created

#### <span style="color:rgb(68, 255, 0)">Foreign Security Principals</span> 
-> FSP is an object created in an AD to represent a security principal that belongs to a trusted external forest. They are created when an object such as user , group or computer from an external forest is added to a group in the current domain. They are created automatically after adding a security principal to a group. Every foreign security principal is a placeholder object that holds the SID of the foreign object. FSPs are created in a specific container named ForeignSecurityPrincipals with a distinguished name like `cn=ForeignSecurityPrincipals,dc=inlanefreight,dc=local`

