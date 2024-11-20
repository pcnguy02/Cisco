# What is it?
MAC Table Attacks is a form of DoS. Threat actors can easily use tools like "macof" to overflow the cisco switch with MAC addresses.  In real time, it is an easy method. According to Cisco a Catalyst 6500 switch can store 132,000 MAC addresses. Tools like "macof" allow flooding
of up to 8,000 fake frames per second. Do the math and your network is down relatively quick. 

# Securing Unused Ports
Securing unused ports should be one of your first steps in securing the switch. Layer 2 devices are considered the weakest link, and layer 2 attacks are some of the easiest for hackers to deploy. 
~~~
Switch(config)# interface fa0/5
Switch(config-if)# shutdown
~~~
~~~
Switch(config)# interface range type module/first-number - last-number
~~~

# Port Security
Enabling port security is one of the simplest and most effective methods for preventing MAC address attacks. This limits the number of valid MAC addresses allowed on a port and allows administrators to manually configure MACs for a port or to permit the switch
to dynamically learn a limited number of MAC addresses. When frames are received, the source MAC is compared to a list of secure source MACs configured by the admin. By default, switch ports are set to dynamic auto (trunking on). 
~~~
S1(config)# interface f0/1
S1(config-if)# switchport port-security
Command rejected: FastEthernet0/1 is a dynamic port.
S1(config-if)# switchport mode access
S1(config-if)# switchport port-security
S1(config-if)# end
S1#
~~~
~~~
S1# show port-security interface f0/1
~~~
Keep in mind that, if you issue the port-security command and more than one device is connected to that port, the port will transition into an error-disabled state. 

# Limit and Learn MAC addresses
Setting Maximum number of MAC Addresses:
~~~
 Switch(config-if)# switchport port-security maximum value
~~~
Default port security value is 1 with a potential maximum of 8192

1. Static MACs
   ~~~
    Switch(config-if)# switchport port-security mac-address mac-address
   ~~~
2. Dynamically Learned MACs
3. Dynamically Learned - Sticky
   Sticky port security allows a switch to dynamically learn MAC addresses and stick them to the running configuration and commits them to NVRAM.
   ~~~
   Switch(config-if)# switchport port-security mac-address sticky
   ~~~
   Verify interface:
   ~~~
   S1# show port-security interface fa0/1
   ~~~
# Port Security Aging
This can be sed to set the aging time for static and dynamic addresses on a port. Use aging to remove secure MAC addresses on a secure
port without manually deleting the existing secure MAC addresses.
- Absolute: Secure addresses on the port are deleted after the specified aging time
- Inactivity: Seucre addresses on the port are deleted only if they are inactive for the specified aging time.
~~~
Switch(config-if)# switchport port-security aging { static | time time | type {absolute | inactivity}}
~~~

# Port Violation Mode
In the event that a MAC address in a port differs from the list of secure addresses, a port violation occurs. By default, ports
enter an error-disabled state. <br>
<br>
Modes:
- shutdown (default)
  - Default state that turns off the port LED, sends a syslog message increments violatin counter, and must be renabled by admin.
- restrict:
  -   Port drops packets with unknown source address until you remove a sufficient number of secure MACs to drop below the max value or increase it.
  -   Increments violation counter and generates syslog message
- protect
  - Least secure of violation modes
  - Drops packets with unknown MAC source addresses until you remove/add sufficient number of secure MACs.
  - No syslog messages.
~~~
Switch(config-if)# switchport port-security violation { protect | restrict | shutdown}
~~~
~~~
S1# show port-security interface f0/1
~~~
# Verify Port Security
It is good practices to check each interface to verify that port 
security is set correctly and to ensure that MAC addresses have been configured correctly. 
<br>
<br>
Port Security for all Interfaces
~~~
S1# show port-security
~~~
Port Security for Specific Interface
~~~
S1# show port-security interface fastethernet 0/1
~~~
Verify learned MAC Addresses for an interface
~~~
S1# show run interface fa0/1
~~~
Verify Secure MAC Addresses
~~~
S1# show port-security address
~~~

# SNMP MAC Address Notification
This feature sends an SNMP trap to the network management station whenever a new MAC address is added to, or an old address
is deleted from the forwarding tables. These are generated only for dynamic and secure MAC addresses. They allow network 
administrators to monitor MAC Addresses that are learned as well as MAC addresses that age out and are removed from the Switch.

~~~
mac address-table notification
~~~
- Used in global configuration mode.









