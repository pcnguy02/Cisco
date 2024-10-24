# Autosecure
Cisco Auto Secure is a feature from CLI that executes a script for simplifying the secure process. The purpose is to make recommendations for fixing security vulnerabilities and modify security configuration. It is generally used to provide a 
baseline security policy on new router and helps secure the management plane. Features can then be altered to support your organization's policy.

Here are some functions/services within the Management plane:
- Secure BOOTP, CDP, FTP, TFTP, PAD, UDP, and TCP small servers, MOP, ICMP (redirects, mask-replies), IP source routing, Finger, password encryption, TCP keepalives, gratuitous ARP, proxy ARP, and directed broadcast
- Legal notification using a banner
- Secure password and login functions
- Secure NTP
- Secure SSH access
- TCP intercept services

Autosecure enables these three forwarding planes:
- Cisco Express Forwarding (CEF)
- Traffic filtering with ACLs
- Cisco IOS firewall inspection for common protocols

# General syntax and options:
// I'd advise performing a full autosecure setup and then altering things based on your needs. 
~~~
Router# auto secure {no-interact | full} [forwarding | management] [ntp | login | ssh | firewall | top-intercept]
~~~

Command Params:
~~~
R1# auto secure ? 
  forwarding   Secure Forwarding Plane
  management   Secure Management Plane
  no-interact  Non-interactive session of AutoSecure
  <cr> 
 
R1#
~~~

# Config Process:
## This first set of code outlines the beginning of the autosecure process 
~~~
R1# auto secure  
  --- AutoSecure Configuration --- 
 
*** AutoSecure configuration enhances the security 
 of the router but it will not make router 
 absolutely secure from all security attacks *** 
 
All the configuration done as part of AutoSecure 
will be shown here. For more details of why and 
how this configuration is useful, and any possible 
side effects, please refer to Cisco documentation of 
AutoSecure. 
 
At any prompt you may enter '?' for help. 
Use ctrl-c to abort this session at any prompt. 
 
~~~

## Step 2:Internet Connection and outside interfaces

~~~
Gathering information about the router for AutoSecure 
 
Is this router connected to internet? [no]: yes 
Enter the number of interfaces facing the internet [1]:  
 
Interface             IP-Address      OK? Method Status                Protocol 
FastEthernet0/0       192.168.10.1    YES manual up                    up       
FastEthernet0/1       192.168.11.1    YES manual up                    up       
FastEthernet0/1/0     unassigned      YES unset  up                    down     
FastEthernet0/1/1     unassigned      YES unset  up                    down     
FastEthernet0/1/2     unassigned      YES unset  up                    down     
FastEthernet0/1/3     nassigned       YES unset  up                    down     
Serial0/0/0           192.168.2.101   YES manual up                    up       
Serial0/0/1           unassigned      YES manual administratively down down     
Vlan1                 unassigned      YES manual up                    down     
Enter the interface name that is facing the internet: Serial 0/0/0 
Invalid interface name 
Enter the interface name that is facing the internet: Serial0/0/0  
 
<continued>
~~~

## Step 3: Disabling Management Plane Services:
~~~
Securing Management plane services... 
 
Disabling service finger 
Disabling service pad 
Disabling udp & tcp small servers 
Enabling service password encryption 
Enabling service tcp-keepalives-in 
Enabling service tcp-keepalives-out 
Disabling the cdp protocol 
 
Disabling the bootp server 
Disabling the http server 
Disabling the finger service 
Disabling source routing 
Disabling gratuitous arp 
 
<continued>
~~~

## Step 4: MOTD Banner
~~~
Here is a sample Security Banner to be shown at every access to device. Modify it 
to suit your enterprise requirements. 
 
Authorized Access only 
  This system is the property of So-&-So-Enterprise.  
  UNAUTHORIZED ACCESS TO THIS DEVICE IS PROHIBITED. 
  You must have explicit permission to access this 
  device. All activities performed on this device 
  are logged. Any violations of access policy will result 
  in disciplinary action. 
 
Enter the security banner {Put the banner between k and k, where k is any character}: 
#
*********     AUTHORIZED ACCESS ONLY ***********
     UNAUTHORIZED ACCESS TO THIS DEVICE IS PROHIBITED.
   You must have explicit permission to access this
   device. Any violations of access policy will result
   in disciplinary action.  
#  
<continued>
~~~
## Step 5: Passwords
// Autosecure, by default, uses enable secret for passwords and login features. This uses MD5. I would using a stronger algorithm. 
~~~
Enable secret is either not configured or is the same as enable password 
Enter the new enable secret: cisco123 
Confirm the enable secret : cisco123 
Enter the new enable password: cisco1 
% Password too short - must be at least 6 characters. Password configuration failed 
Enter the new enable password: cisco321 
Confirm the enable password: cisco321 
Configuring AAA local authentication 
Configuring Console, Aux and VTY lines for local authentication, exec-timeout, 
and transport 
Securing device against Login Attacks 
Configure the following parameters 
 
Blocking Period when Login Attack detected: 120 
Maximum Login failures with the device: 2 
Maximum time period for crossing the failed login attempts: 60 
 
Configure SSH server? [yes]: y 
 
<continued>
~~~
## Step 5: Securing Interfaces
~~~
Configuring interface specific AutoSecure services 
Disabling the following ip services on all interfaces: 
 
 no ip redirects 
 no ip proxy-arp 
 no ip unreachables 
 no ip directed-broadcast 
 no ip mask-reply 
Disabling mop on Ethernet interfaces 
 
<continued>
~~~
## Step 6: Securing the Forwarding Plane:
// CBAC stands for Context-Based Access Control and is a feature of the Cisco IOS Firewall. This feature actively inspects activity behind a firewall and specifies what traffic needs to be let in and what traffic needs to be let out by using ACLs.
// It is similar to normal ACLs but it includes IP inspect statements that allow the inspection of the protocol to make sure nothing is tampered with before the protocol goes to the systems behind the firewall. 
~~~
Securing Forwarding plane services... 
 
Enabling CEF (This might impact the memory requirements for your platform) 
Enabling unicast rpf on all interfaces connected to internet 
 
Configure CBAC Firewall feature? [yes/no]: yes
~~~
