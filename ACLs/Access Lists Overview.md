# Access Control Lists

### - In networking we use ACL's for a variety of reasons. ACL's are typically used to filter traffic on an interface. ACL's on Cisco iOS can filter based on 
    - IP address
    - Protocols
    - Port numbers

### - ACL's can be used for other reasons than just filtering traffic on a link. ACL's can also be used to simply identify data traffic that can than be used for other technologies/protocols. Some examples are QoS, Route Filtering, Route Redistribution, NAT and zone-based firewalls.

### - On Cisco iOS ACL's come in a couple different flavors. Standard, extended, and named.

![](/ACLs/ACL_image.png)

# Standard ACLs

### - Standard ACLs will only let you filter based on the source IP address. Standards ACL numbers range from 1-99, 1399 - 1999.

### - Standard ACLs best practice is too apply the ACL as close to the destination as possible. The ACEs (Access Control Entries) on standard ACLs will only be based on source IP address.

![](/ACLs/standard_acl_image.png)

# Extended ACls

### - Extended ACLs give network administrators more granular control over what they can permit/deny. Extended ACLs allow filtering based protocol and port numbers.

### - Extended ACLs numbers range from 100-199 and 2000 - 2699.

### - Extended ACLs best practice is too apply the ACL as close to the source as possible. Acesss Control Entries in extended ACLs can be based on source/destination IP, src/dst protocol, and port number.

![](/ACLs/extended_acl_iamge.png)

# Named ACLs

### - Named ACLs can be either standard or extended and the main difference is the syntax difference, and how you can edit this ACL on the Cisco iOS.

### - Named ACLs do not need to be specified by a number, they are created and specified using a **"name"** you create as the administrator.
