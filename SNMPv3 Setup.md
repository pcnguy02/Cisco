# SNMP 
SNMP is known as Simple Network Management Protocol and allows network administrators to manage servers, workstations, routers, switches and 
security appliances on an IP network. It enables admins to monitor and manage network performance, 
find and solve network problems and plan for network growth. There should be at least one SNMP manager within your topology 

Elements:
- SNMP Manager
   - Uses SNMP agent to access info within MIB 
- SNMP Agents (managed nodes)
  - Collect info on managed device and its operations
- Management Information Base (MIB)
   - Stores information from agent locally
 
  #SNMPv3 Setup
  Step 1: Configure ACL permitting access to authorized SNMP Managers
  ~~~
  Router(config)# ip access-list acl-name
  Router(config-std-nacl)# permit source_net
  ~~~
  Step 2: Configure SNMP view to identify MIB Object IDs
  ~~~
   Router(config)# snmp-server view view-name oid-tree
  ~~~
  Step 3: Configure SNMP group features:
   - Configure a name for the group.
   - Set the SNMP version to 3 with the v3 keyword.
   - Require authentication and encryption with the priv keyword.
   - Associate a view to the group and give it read only access with the read command.
   - Specify the ACL configured in Step 1.
  ~~~
   Router(config)# snmp-server group group-name v3 priv read view-name access [acl-number | acl-name]
  ~~~
  Step 4: Configure SNMP group user features with:
-  Configure a username and associate the user with the group name configured in Step 3.
- Set the SNMP version to 3 with the v3 keyword.
-  Set the authentication type to either md5 or sha and configure an authentication password. SHA is preferred and should be supported by the SNMP management software.
-  Require encryption with the priv keyword and configure an encryption password.

~~~
 Router(config)# snmp-server user username group-name v3 auth {md5 | sha} auth-password priv {des | 3des | aes {128 | 192 | 256}} priv-password
~~~

# SNMP Verification
Example with code: 
~~~
R1# show run | include snmp

snmp-server group ADMIN v3 priv read SNMP-RO access PERMIT-ADMIN 
snmp-server view SNMP-RO iso included

R1# show snmp user

User name: BOB 
Engine ID: 80000009030030F70DA30DA0 
storage-type: nonvolatile active 
Authentication Protocol: SHA 
Privacy Protocol: AES128 
Group-name: ADMIN
~~~

ManageEngine offers a free SNMP MIB Browser for further verification. Configure the tool with the user details used in SNMP and test if it can access the agent. 
I'd also recommend verifying that data is encrypted by capturing SNMP packets through Wireshark
