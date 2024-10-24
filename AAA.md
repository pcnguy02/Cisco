# Info (NOT DONE)
Standard password procedures like the one below are considered weak and insecure.
~~~
R1(config)# line vty 0 4
R1(config-line)# password cis5cio
R1(config-line)# login
~~~
It's the easiest method to implement, but it doesn't provide accountability. 

# AAA Componenets
- Authentication
  - Proving identity before accessing the network and resources. Established using Username and Passwords, challenges/responses, token cards...
- Authorization
  - Determines which resources the user can access and which operations the user is allowed to perform
- Accounting and Auditing
  - Logs what the user does, accesses, amount of time a resource is accessed and changes made

# Authentication Modes
- Local AAA
   - Uses a local database for authentication. It stores usernames and passwords locally on the Cisco router and users authenticate against the database. Ideal for small networks
- Server-Based AAA
  - Router accesses a central AAA server which contains credentials for all users. Uses RADIUS or TACACS+ protocols to communicate with the AAA server. Generally used for locations with multiple routers and switches.
 

# Configuring Local AAA
~~~
R1(config)# username JR-ADMIN algorithm-type scrypt secret Str0ng5rPa55w0rd
R1(config)# username ADMIN algorithm-type scrypt secret Str0ng5rPa55w0rd  
R1(config)# aaa new-model
R1(config)# aaa authentication login default local-case
R1(config)#
~~~
