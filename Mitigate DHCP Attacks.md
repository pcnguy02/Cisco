# Types of DHCP Attacks
1. Starvation Attack
   - Attack with a goal for DoS for connecting clients. It requires tools such as Gobbler.
2. Spoofing
   - Occurs when a rogue DHCP server is connected to the network and provides false IP config parameters to legit clients.
   - Ways a rogue server can provide misleading info
      - Wrong default gateway
      - Wrong DNS server
      - Wrong IP address
    
# DHCP Snooping
Snooping mitigates DHCP starvation by rate limiting the number of DHCP discovery messages that an untrusted port can receive. It builds and maintains a snooping database that a switch can use to filter DHCP messages from untrusted sources.
The table includes client MAC, IP, DHCP lease time, binding type, VLAN number, and interface info. 

Steps to Implement:
- Step 1. Enable DHCP snooping by using the ip dhcp snooping global configuration command.
- Step 2. On trusted ports, use the ip dhcp snooping trust interface configuration command.
- Step 3. Limit the number of DHCP discovery messages that can be received per second on untrusted ports by using the ip dhcp snooping limit rate interface configuration command.
- Step 4. Enable DHCP snooping by VLAN, or by a range of VLANs, by using the ip dhcp snooping vlan global configuration command.
