![[Pasted image 20250903102153.png]]

## Pre-Engagement
-> Stage where the main commitments,tasks,scope, limitation, and related agreements are documented in writing.
![[Pasted image 20250903103419.png]]

## Information Gathering
-> Information Gathering is an essential part of any assessment. Because the knowledge gained from it, the conclusions we draw and the steps we take are based on the information available. This information must be obtained from somewhere, so it is critical to know how to retrieve it and best leverage it based on our assessment goals.

![[Pasted image 20250903103623.png]]

## Vulnerability Assessment
-> Vulnerability Assessment involves two parts: Automated scanning for known issues and creative analysis to uncover potential weaknesses. While tools match systems against known vulnerabilities, real value comes from thinking outside the box, connecting information, spotting gaps, and understanding processes to identify ways attackers could gain unintended access or privileges.

![[Pasted image 20250903125425.png]]

From this stage, there are four paths we can take, depending on how far we have come:

|**Path**|**Description**|
|---|---|
|`Exploitation`|The first we can jump into is the `Exploitation` stage. This happens when we do not yet have access to a system or application. Of course, this assumes that we have already identified at least one gap and prepared everything necessary to attempt to exploit it.|
|`Post-Exploitation`|The second way leads to the `Post-Exploitation` stage, where we escalate privileges on the target system. This assumes that we are already on the target system and can interact with it.|
|`Lateral Movement`|Our third option is the `Lateral Movement` stage, where we move from the already exploited system through the network and attack other systems. Again, this assumes that we are already on a target system and can interact with it. However, privilege escalation is not strictly necessary because interacting with the system already allows us to move further in the network under certain circumstances. Other times we will need to escalate privileges before moving laterally. Every assessment is different.|
|`Information Gathering`|The last option is returning to the `Information Gathering` stage when we do not have enough information on hand. Here we can dig deeper to find more information that will give us a more accurate view.|

## Exploitation
-> At this stage we will exploit the target get a foothold on the target.

![[Pasted image 20250903125512.png]]

|**Path**|**Description**|
|---|---|
|`Information Gathering`|Once we have initial access to the target system, regardless of how high our privileges are at that moment, we need to gather information about the local system. Whether we use this new information for privilege escalation, lateral movement, or data exfiltration does not matter. Therefore, before we can take any further steps, we need to find out what we are dealing with. This inevitably takes us to the vulnerability assessment stage, where we analyze and evaluate the information we find.|
|`Post-Exploitation`|`Post-exploitation` is mainly about escalating privileges if we have not yet attained the highest possible rights on the target host. As we know, more opportunities are open to us with higher privileges. This path actually includes the stages `Information Gathering`, `Vulnerability Assessment`, `Exploitation`, and `Lateral Movement` but from an internal perspective on the target system. The direct jump to post-exploitation is less frequent, but it does happen. Because through the exploitation stage, we may already have obtained the highest privileges, and from here on, we start again at `Information Gathering`.|
|`Lateral Movement`|From here, we can also skip directly over to `Lateral Movement`. This can come under different conditions. If we have achieved the highest privileges on a dual-homed system used to connect two networks, we can likely use this host to start enumerating hosts that were not previously available to us.|
|`Proof-of-Concept`|We can take the last path after gaining the highest privileges by exploiting an internal system. Of course, we do not necessarily have to have taken over all systems. However, if we have gained the Domain Admin privileges in an Active Directory environment, we can likely move freely across the entire network and perform any actions we can imagine. So we can create the `Proof-of-Concept` from our notes to detail and potentially automate the paths and activities and make them available to the technical department.|

## Post Exploitation
-> We will further find more information about the foothold we got, information gathering and then move forward to lateral movement.

![[Pasted image 20250903125639.png]]

## Lateral Movement
-> Here we will exploit other hosts present in the network to escalate our privileges to the highest possible.

![[Pasted image 20250903125726.png]]

## Proof-of-Concept
-> PoC here we'll have to document each and every step from starting to exploit the target.

