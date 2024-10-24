# Not Done 
# What is an ACL?
An ACL is a series of commands used to filter packets based on information within the packet header. Routers, by default, do not have any ACLs configured. 
When network traffic passes through an interface using ACLs, the router compares information within the packet against each ACE in sequential order. 

# Packet Filtering
Packet filtering controls access to a network through analysis of incoming/outgoing packets and permitted or denying them based on the packet criteria. This can occur at Layer 3 or Layer 4 of the OSI model. 
Cisco Router support two types of ACLs:
- Standard
  - Only filter at layer 3 using source IPv4 address only
- Extended
  - Filters at layer 3 using the source and/or destination IPv4 address. It can filter at layer 4 using TCP, UDP and optional protocol type info for finer control.
 
# Configuring ACLs
For ACL config, I recommend creating named ACLs. Using numbered ACLs is an option. However, it is easier to understand the function of the ACL when you have a name for it. Be mindful of ACL layout as it is a top-down structure. 

- Standard ACL: 
~~~
Router(config)# ip access-list standard access-list-name
~~~
- Extended ACL:
~~~
 Router(config)# ip access-list extended access-list-name
 R1(config-ext-nacl)# 
~~~
