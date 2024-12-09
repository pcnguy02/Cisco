# ARP Attacks
ARP Attacks occur when an attacker sends a gratuitous ARP message containing a spoofed MAC to a switch and the switch updates its MAC table accordingly. As a result, any host can claim ownership of an IP and MAC address combo they choose. 

# Dynamic ARP Inspection
Method of ARP attack mitigation. Here are how it prevents them:

- Not relaying invalid or gratuitous ARP Requests out to other ports in the same VLAN
- Intercepting all ARP Requests and Replies on untrusted ports
- Verifying each intercepted packet for a valid IP-to-MAC binding
- Dropping and logging ARP Requests coming from invalid sources to prevent ARP poisoning
- Error-disabling the interface if the configured DAI number of ARP packets is exceeded

# DAI Guidelines
1. Enable DHCP snooping globally.
2. Enable DHCP snooping on selected VLANs.
3. Enable DAI on selected VLANs.
4. Configure trusted interfaces for DHCP snooping and ARP inspection. 

~~~
S1(config)# ip dhcp snooping
S1(config)# ip dhcp snooping vlan 10
S1(config)# ip arp inspection vlan 10
S1(config)# interface fa0/24
S1(config-if)# ip dhcp snooping trust
S1(config-if)# ip arp inspection trust
~~~
DAI can also be configured to check for destination, source MACs and IP addresses. 
