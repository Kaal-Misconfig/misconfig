+++
title = "AD Functionality"
summary = "AD Functionality and its roles and Trusts"
date = 2025-11-21
+++

## The 5 <span style="color:rgb(68, 255, 0)">FSMO</span> Roles

1. **Schema Master**
   -> This role manages the read/write copy of the AD schema, which defines all attributes that can apply to an object in AD

2. **Domain Naming Master**
   -> Manages Domain names and ensures that two domains of the same name are not created in the same forest.

3. **Relative ID**
   -> The RID Master assigns blocks of RIDs to other DCs within the domain that can be used for new objects. The RID Master helps ensure that multiple objects are not assigned the same SID. Domain object SIDs are the domain SIDs combined with the RID number assigned to the object to make the unique SID

4. **PDC Emulator**
   -> The host with this role would be the authoritative DC in the Domain and respond to authentication requests, password changes, and manage Group Policy Objects. The PDC Emulator also maintains time within the domain.

5. **Infrastructure Master**
   -> This role translates GUIDs, SIDs, and DNs between domains. This role is used in organization with multiple domains in a single forest. The infrastructure master helps them to communicate. If this role is not functioning properly, ACL will show SIDs instead of fully resolved names


## <span style="color:rgb(68, 255, 0)">Trusts</span> 
###### Trust is used to establish <span style="color:rgb(68, 255, 0)">forest-forest</span> or <span style="color:rgb(68, 255, 0)">domain-domain</span> authentication, allowing users to access resources in (or administer) another domain outside of the domain their account resides in. A trust creates a link between the authentication systems of two domains.

1. **Parent-child**
   -> Domains within same forest. The child domain has two-way transitive trust with the parent domain

2. **Cross-link**
   -> A trust between child domains to speed up authentication 

3. **External**
   -> A non-transitive trust between two separate domains in separate forests which are not already joined by a forest trust. This type pf trust utilizes SID filtering.

4. **Tree-root**
   -> A two-way transitive trust between a forest root domain and a new tree root domain. They are created by design when you set up a new tree root domain within a forest

5. **Forest**
   -> A transitive trust between two forest root domains

