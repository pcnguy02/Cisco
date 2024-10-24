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

