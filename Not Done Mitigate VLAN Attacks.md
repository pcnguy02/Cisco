# What are VLANs
VLANs are used to create separate broadcast domains on switches. Endpoints located in one VLAN are unable to communicate with endpoints
in another VLAN unless permitted to do so by a router or Layer 3 switch. That being said, VLANs can be used to separate sensitive content from network
traffic. 

# VLAN Hopping
VLAN Hopping is one attack method from threat actors. This enables traffic from one VLAN to be seen by another VLAN without 
the aid of a router. Threat actors configure a host to act like a switch to take advantage of the automatic trunking port feature
enabled by default on most switch ports. 

# VLAN Double-Tagging
