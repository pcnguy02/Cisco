# Configure Password
- Line Console 0
~~~
Sw-Floor-1# configure terminal
Sw-Floor-1(config)# line console 0
Sw-Floor-1(config-line)# password cisco
Sw-Floor-1(config-line)# login
Sw-Floor-1(config-line)# end
Sw-Floor-1#
~~~

- VTY Lines
~~~
Sw-Floor-1# configure terminal
Sw-Floor-1(config)# line vty 0 15
Sw-Floor-1(config-line)# password cisco
Sw-Floor-1(config-line)# login
Sw-Floor-1(config-line)# end
Sw-Floor-1
~~~
- Password Encryption, Min-length, and User account with SCRYPT
~~~
R2(config)#service password-encryption
R2(config)#security passwords min-length 10
R2(config)#username JR-ADMIN algorithm-type scrypt secret cisco12345
~~~

# Virtual Login Enhancements
- MOTD (LOGIN BANNER)
~~~
Router(config)# banner {  motd | exec | login } delimiter message delimiter
~~~
- Login Block (Defends against DoS by disabling logins after failed attempts)
~~~
R1(config)# login block-for SECONDS_BLOCKED attempts MADE_ATTEMPTS within _seconds_
~~~
- Login Quiet-Mode (Maps to ACL and identifies permitted hosts. Ensures only authorized hosts)
~~~
Quiet-Mode blocks all login attempts using Telnet, SSH, and HTTP.
Normal-Mode keeps count of the number of failed login attempts within an identified amount of time.
R1(config)# ip access-list standard PERMIT-ADMIN
R1(config-std-nacl)# remark Permit only Administrative hosts    
R1(config-std-nacl)# permit YOUR_IP
R1(config-std-nacl)# permit YOUR_IP
R1(config-std-nacl)# exit
R1(config)# login quiet-mode access-class PERMIT-ADMIN
R1(config)# login delay 3 
~~~
- Logging Failed Attempts
~~~
Router(config)# login on-success log [every login]
Router(config)# login on-failure log [every login]
~~~
- Security Auth Threshold Log
~~~
Router(config)# security authentication failure rate threshold-rate log
~~~
- Show Login (Shows login Settings)
~~~
R1# show login
~~~

# Configuring SSH
- hostname
  ~~~
  Router# configure terminal
  Router(config)# hostname R1
  ~~~
- Configure IP Domain Name
  ~~~
  R1(config)# ip domain name span.com
  ~~~
- Generate key to encrypt SSh Traffic
~~~
R1(config)# crypto key generate rsa general-keys modulus KEY_SIZE
~~~
- Verify or create local database entry
~~~
R1# show crypto key mypubkey rsa
~~~
- Authenticate against local database
- Enable VTY inbound SSH Sessions (Disabled by default)
~~~
R1(config)# line vty 0 4
R1(config-line)# login local
R1(config-line)# transport input ssh
R1(config-line)# exit
~~~

# SSH Login Enhancements
- Show IP SSH
~~~
R1# show ip ssh
~~~
- SSH Timeout & Authentication
~~~
ip ssh time-out SECONDS
ip ssh authentication-retries
~~~
- Show current SSH Conns
~~~
R1# show ssh
~~~
