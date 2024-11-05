# Traffic Mirroring and SPAN Info  
Switches segment networks, and, as a result, limit the amount of traffic visible to network monitoring devices. However, it is important to monitor all traffic. Special techniques must be used to bypass segmentation from network switches. Port mirroring is one technique
supported by many enterprise switches. It enables the switch to copy frames that are received on one or more ports to a Switch Port Analyzer (SPAN) that is connected to an analysis device.

<br>Terms:
1. Ingress traffic
   - Traffic entering a switch
3. Egress traffic
   - Traffic leaving a switch
5. Source (SPAN) port
   - Source ports monitored as traffic entering them is mirrored to destination ports
7. Destination (SPAN) port
   - Port that mirrors source ports. Often connects to analysis devices (packet analyzers or IDSs)
  
# Configuring Cisco SPAN
~~~
 Switch(config)# monitor session number source [interface interface | vlan vlan]
~~~
~~~
 Switch(config)# monitor session number destination [interface interface | vlan vlan]
~~~
~~~
  S1# show monitor
~~~
   
