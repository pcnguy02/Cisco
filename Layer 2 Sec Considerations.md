# Vulnerabilities and Attack Categories
The OSI model is a great reference for understanding networks. Security is only as strong as the weakest link. That being said,
layer 2 is compromised, every layer above it is too. Here are some vulnerabilities against Layer 2 LANs:

1. MAC Table
   - MAC table overflow
3. VLAN Attacks
   - VLAN Hopping and VLAN double-tagging
5. DHCP
   - DHCP Starvation and spoofing
7. ARP
   - ARP Spoofing and Poisoning
9. Spoofing
    - MAC and IP Spoofing
11. Spanning Tree
    - Manipulation attacks
# Switch Mitigation Topics
- Port Security
- DHCP Snooping
- Dynamic Arp Inspection (DAI)
- IP Source Guard (IPSG)

# MAC Table Attacks 
MAC addresses, in switches, are used to forward frames to other devices on a network. Ethernet switches use MAC addresses for forwarding 
decisions and are unaware of the protocols being carried in the data portion of the frame. 
