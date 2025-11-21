+++
title = "Active Directory Structure"
summary = "Read more.."
+++
-> Active Directory is a directory service for Windows Network Environments, It is a distributed, hierarchical structure that allows for centralized management of an organization's resources, including users, computers, groups, network devices, and file shares, group policies, server and workstations

- Active Directory is arranged in hierarchical tree structure, with a forest at the top containing one or more domains, which can themselves, have nested subdomains. A forest is the security boundary within which  all objects are under administrative control, A forest may contain multiple domains and a domain may include further child or subdomains. A domain is a structure within which constrained objects (users, computers, and groups) are accessible. It has many built-in organizational units, such as Domain Controllers, Users, Computers and new OUs can be created as required. OUs may contain objects and sub-OUs, allowing for the assignment of different group policies
 
![[Pasted image 20250723121921.png]]

<span style="color:rgb(68, 255, 0)">INLANEFREIGHT.LOCAL/</span> is the root domain and contains the subdomains (either child or tree root domains) <span style="color:rgb(68, 255, 0)">ADMIN.INLANEFREIGHT.LOCAL</span>, <span style="color:rgb(68, 255, 0)">CORP</span>, <span style="color:rgb(68, 255, 0)">INLANEFREIGHT.LOCAL</span> and <span style="color:rgb(68, 255, 0)">DEV.INLANEFREIGHT.LOCAL</span> as well as the other objects that make up a domain such as users, groups, computers and more, 

![[Pasted image 20250723122354.png]]

the two-way arrow between <span style="color:rgb(68, 255, 0)">inlanefreight.local</span> and <span style="color:rgb(68, 255, 0)">freightlogistics.local</span> shows a <span style="color:rgb(68, 255, 0)">trust relationship</span>, meaning that users in <span style="color:rgb(68, 255, 0)">INLANEFREIGHT.LOCAL</span> can access resources in <span style="color:rgb(68, 255, 0)">FREIGHTLOGISTICS.LOCAL</span> and vice versa. But child domains in Forest A do not necessarily have trusts established with he child domains in Forest B. This means that a user that is part of <span style="color:rgb(68, 255, 0)">admin.dev.freightlogistics.local</span> would NOT be able to authenticate to machines in the <span style="color:rgb(68, 255, 0)">wh.corp.inlanefreight.local</span> domain by default even though a bidirectional trust exists between top level <span style="color:rgb(68, 255, 0)">inlanefreight.local</span> and <span style="color:rgb(68, 255, 0)">freightlogistics.local </span>domains. To allow direct communication from `admin.dev.freightlogistics.local` and `wh.corp.inlanefreight.local`, another trust would need to be set up.

