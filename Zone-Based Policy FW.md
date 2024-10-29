# Zone-Based Policy FW 
Cisco IOS Firewalls have two configuration models: Classic FW and Zone-based Policy Firewall (ZPF). ZPF is a configuration model used to assign interfaces 
to a security zone an using firewall policies to traffic moving between the zones. The first approach (classic) is traditional and applies policy on interfaces. ZPF provides structure and is useful for documentation and communication.
Overall, it makes network security implementations accessible and easy to use. Here are the steps:
1. Determine zones
2. Establish policies between zones
3. Design physical infrastructure
4. Identify subnets within zones and merge traffic requirements

# ZPF Actions
Includes:
1. Inspect - Performs stateful packet inspection
2. Drop - Analogous to deny in an ACL. A _log_ option is available to log rejected packets
3. Pass - Analogous to a permit statement in ACL. Pass actions do not track the state of connections or sessions within the traffic.

# Configure ZPF
Step 1: Create Zones 
~~~
Router(config)# zone security zone-name

R1(config)# zone security PRIVATE 
R1(config-sec-zone)# exit
R1(config)# zone security PUBLIC 
R1(config-sec-zone)# exit
R1(config)#
~~~
Step 2: Identify Traffic <br>
Use class-maps to identify traffic to which policy can be applied. Classes are a way of identifying a set of packets based on contents using match conditions. Classes are generally defined so that you can apply an action to specific traffic that reflect policy. 
~~~
Router(config)# class-map type inspect [match-any | match-all] _class-map-name_
~~~
Params:
1. match-any (Packets must meet one of the match criteria to be considered a member)
2. match-all (Packets must meet all criteria)

1. match access-group
   - Configure map based on specified ACL name or number. 
2. match protocol
   - Configure match based on specified protocols
3. match class-map
   - Uses another class-map to identify traffic<br>

Step 3: Define Actions <br>
Use policy-map to define what actions should be taken for traffic that is a member of a class. 

1. inspect
   - Action offers state-based traffic control. Router maintains session information for TCP and UDP and permits return traffic. 
2. drop
   - Discards unwanted traffic
3. pass
    - Stateless action allowing the router to forward traffic from one zone to another <br>

~~~
R1(config)# policy-map type inspect policy-map-name
R1(config-pmap)# class type inspect class-map-name
R1(config-pmap-c)# {inspect | drop | pass}
~~~
    
Step 4: Identify Zone-Pair and Match to Policy.
~~~
Router(config)# zone-pair security zone-pair-name source {source-zone-name | self} destination {destination-zone-name | self}
Router(config-sec-zone-pair)# service-policy type inspect policy-map-name
~~~

Params:
1. source source-zone-name
  - specifies name of zone from which traffic is originating<br>
2. destination
  - specifies name of the zone to which traffic is destined
3. self
  - Specifies system-defined zone and indicates whether traffic will be going to or from the router itself. 
<br>
Step 5: Assign Zones to Interfaces<br>
This is assigning proper interfaces to a specified zones. Server-policy immediately applies once assigned. However, if there is no server-policy, all transit traffic will be dropped.
<br>

~~~
Router(config-if)# zone-member security zone-name
~~~
Example:
~~~
R1(config)# interface GigabitEthernet 0/0
R1(config-if)# zone-member security PRIVATE
R1(config-if)# interface Serial 0/0/0
R1(config-if)# zone-member security PUBLIC
~~~

# Considerations: 
When configuring ZPF with CLI, you should consider:
- The router never filters the traffic between interfaces in the same zone.
- An interface cannot belong to multiple zones. To create a union of security zones, specify a new zone and appropriate policy map and zone pairs.
- ZPF can coexist with Classic Firewall although they cannot be used on the same interface. Remove the ip inspect interface configuration command before applying the zone-member security command.
- Traffic can never flow between an interface assigned to a zone and an interface without a zone assignment. Applying the zone-member configuration command always results in a temporary interruption of service until the other zone-member is configured.
- The default inter-zone policy is to drop all traffic unless otherwise specifically allowed by the service-policy configured for the zone-pair.
- The zone-member command does not protect the router itself (traffic to and from the router is not affected) unless the zone- pairs are configured using the predefined self zone.
