## Testing Methods

##### <span style="color:rgb(129, 249, 31)">External</span> or <span style="color:rgb(129, 249, 31)">Internal</span> 

#### External Penetration Test
-> Pentests are often done externally to test defenses against internet-based attacks. Testing can be from our host (via VPN) or a VPS. Some clients don't care about stealth, while other want quiet approaches to evade firewalls, IDS/IPS, or alarms. A hybrid method may also be used, starting stealthy and getting noisier to test detection. The ultimate goal is to compromise external hosts, extract sensitive data, or pivot into the internal network.

#### Internal Penetration Test
-> Internal pentest is when we perform testing from within the corporate network. This stage may be executed after successfully penetrating the corporate network via the external pentest or starting from an assumed breach scenario.

## Types of Penetration Testing

|**Type**|**Information Provided**|
|---|---|
|`Blackbox`|`Minimal`. Only the essential information, such as IP addresses and domains, is provided.|
|`Greybox`|`Extended`. In this case, we are provided with additional information, such as specific URLs, hostnames, subnets, and similar.|
|`Whitebox`|`Maximum`. Here everything is disclosed to us. This gives us an internal view of the entire structure, which allows us to prepare an attack using internal information. We may be given detailed configurations, admin credentials, web application source code, etc.|
|`Red-Teaming`|May include physical testing and social engineering, among other things. Can be combined with any of the above types.|
|`Purple-Teaming`|It can be combined with any of the above types. However, it focuses on working closely with the defenders.|

## Types of Testing Environments

| Network | Web App | Mobile            | API               | Thick Clients |
| ------- | ------- | ----------------- | ----------------- | ------------- |
| IoT     | Cloud   | Source Code       | Physical Security | Employees     |
| Hosts   | Server  | Security Policies | Firewalls         | IDS/IPS       |

## Precautionary Measures during Penetration Tests

| **  <br>Precautionary Measure** |                                                                                                                                                                |
| ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `☐`                             | Obtain written consent from the owner or authorized representative of the computer or network being tested                                                     |
| `☐`                             | Conduct the testing within the scope of the consent obtained only and respect any limitations specified                                                        |
| `☐`                             | Take measures to prevent causing damage to the systems or networks being tested                                                                                |
| `☐`                             | Do not access, use or disclose personal data or any other information obtained during the testing without permission                                           |
| `☐`                             | Do not intercept electronic communications without the consent of one of the parties to the communication                                                      |
| `☐`                             | Do not conduct testing on systems or networks that are covered by the Health Insurance Portability and Accountability Act (HIPAA) without proper authorization |

