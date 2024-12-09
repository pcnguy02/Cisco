# What are VLANs
VLANs are used to create separate broadcast domains on switches. Endpoints located in one VLAN are unable to communicate with endpoints
in another VLAN unless permitted to do so by a router or Layer 3 switch. That being said, VLANs can be used to separate sensitive content from network
traffic. 

# VLAN Hopping
VLAN Hopping is one attack method from threat actors. This enables traffic from one VLAN to be seen by another VLAN without 
the aid of a router. Threat actors configure a host to act like a switch to take advantage of the automatic trunking port feature
enabled by default on most switch ports. 

# VLAN Double-Tagging
Double-tagging is a unidirectional attack and works only when an attacker is connected to a port residing in the same VLAN as the native VLAN of the trunk port. Essentially, it allows attackers to send data to hosts or servers on a VLAN that would otherwise be blocked
by some type of access control config. 

Mitigation Methods for Double-Tagging:
- Disable trunking on all access ports.
- Disable auto trunking on trunk links so that trunks must be manually enabled.
- Be sure that the native VLAN is only used for trunk links.

Mitigating VLAN Hopping Attacks:
- Step 1: Disable DTP (auto trunking) negotiations on non-trunking ports by using the switchport mode access interface configuration command.
- Step 2: Disable unused ports and put them in an unused VLAN. In the example it is VLAN 1000.
- Step 3: Manually enable the trunk link on a trunking port by using the switchport mode trunk command.
- Step 4: Disable DTP (auto trunking) negotiations on trunking ports by using the switchport nonegotiate command.
- Step 5: Set the native VLAN to a VLAN other than VLAN 1 by using the switchport trunk native vlan vlan_number command.

# Private VLANs
VLANs are broadcast domains but, in some situations, it's useful to break this rule and allow minimum required L2 connectivity within the VLAN. Private VLANs provide L2 isolation between ports within the same broadcast domain. Here are 3 PVLAN port types:
- Promiscuous
  - A promiscuous port can talk to everyone. It can communicate with all interfaces, including the isolated and community ports within a PVLAN.
- Isolated
  - An isolated port can only talk to promiscuous ports. An isolated port has complete Layer 2 separation from the other ports within the same PVLAN, but not from the promiscuous ports. PVLANs block all traffic to isolated ports except traffic from promiscuous ports. Traffic from an isolated port is forwarded only to promiscuous ports.
- Community
  - Community ports can talk to other community and promiscuous ports. These interfaces are separated at Layer 2 from all other interfaces in other communities or isolated ports within their PVLAN.
