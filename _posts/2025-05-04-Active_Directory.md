---
title: Active Directory Penetration Testing
description: Active Directory Zero To Hero 
date: 2025-05-04 03:00:00 -0500
categories: [AD,Penetration Testing]
tags: [Nmap]
pin: true
math: true
mermaid: true
image:
  path: https://miro.medium.com/v2/resize:fit:1400/format:webp/1*5DF1f_DamiK-eY7gwsKpog.png
---
# <font color="red"><strong>Active Directory Basics</strong></font>
## <font color="black"><strong>AD Components :</strong></font>
- **Physical**: 
  - Domain Controllers : is what control everything (DC)
  - Data store :  Contain the database files , information of users , services and applications .    (DS) - contain the ntds.dit (⛔ file) 
- **Logical**: 
  - Objects : - class object : users , computer…. - Attributes : the name 
  - Domain : unknwn.*** ….
  - Tree : contains subdomains and domain …
  <img src="https://miro.medium.com/v2/resize:fit:4800/format:webp/0*18H4GCrDER3FlGG7" width="500" height="500" alt="">
  - Forest : collection of trees 
  - Organizational Units (OUs) : it’s containers that contain users , groups , computers …
  - Trusts : provide a mechanisme to gain access to ressources in another domain .
  <img src="https://raw.githubusercontent.com/unkn0wnB0y1/unkn0wnB0y1.github.io/refs/heads/main/assets/Img/Active_Directory/1.png" width="500" height="500" alt="">
  # <font color="red"><strong>Initial Attack Vectors On Active Directory</strong></font>
Now we will move on to something more challenging — this is the main goal of this blog.
## <font color="Black"><strong>LLMNR Poisoning :</strong></font>
### <font color="green"><strong>What is LLMNR ?</strong></font>
**LLMNR** is a protocol used by Windows (and sometimes Linux) systems to resolve hostnames not resolved via DNS.
### <font color="green"><strong>What is LLMNR Poisonning ?</strong></font>
The objective of the **LLMNR Poisonning** is to Respond to LLMNR requests with a fake response, making the victim believe we are the machine they are looking for → capture the credentials (NTLMv2 hashes) they send.
<img src="https://raw.githubusercontent.com/unkn0wnB0y1/unkn0wnB0y1.github.io/refs/heads/main/assets/Img/Active_Directory/2.png" width="500" height="500" alt="">

### <font color="green"><strong>Defending Against LLMNR Poisoning Attacks :</strong></font>
**The most effective defense against LLMNR poisoning is to disable LLMNR and NBT-NS entirely across the network.**

If an organization must use LLMNR for compatibility reasons, it is strongly recommended to:
- Implement network access control (e.g., 802.1X, VLAN segmentation) to limit attacker access.
- Enforce strong password policies to make captured NTLMv2 hashes more resistant to cracking.

## <font color="Black"><strong>SMB Relay :</strong></font>