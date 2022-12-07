# Port Security

### Port Security is a Layer 2 Security protocol that protects the Switch from CAM/MAC address flooding. Port Security will be enabled per-interface on L2 switches. Port-security by default will shutdown a port and place it into **"err-disabled"** mode. Port-security can only be enabled on **"access"** ports. By default port-security will only 1 MAC address per interface.

![](/Layer%202%20Security/layer_2_security_network_diagram.png)

### For this How To we will first configure the trunks, VLANs and access ports. If you do not know how to configure trunks, VLANs and access ports refer to our other How To's.

`SW1(config)#interface range eth0/1, eth0/3` # This command brings us into the range-sub-interface mode.

`SW1(config-if-range)#switchport port-security` # This command will enable **"port-security"** on the interface

`SW1(config-if-range)#switchport port-security maximum 2` # This command will set the amount of MAC addresses allowed on the interface

`SW1(config-if-range)#switchport port-security mac-address sticky` # This command will apply the connected SRC MAC address to the running-configuration of the interface.

### The full configuration is shown below

![](/Layer%202%20Security/port_security_config.png)

### Verficaition

`SW1#show run interface ethernet0/3` # This command will show you the running configuration of the interface

`SW1#show port-security` # This command will show you the port-security table. This table shows you which ports are configured for port-security.

![](/Layer%202%20Security/show_port_security_cmd.png)

`SW1#show port-security interface ethernet0/1` # This command will show you the individual ports and how they are configured for port-security.

![](/Layer%202%20Security/show_port_security_interface_eth0.png)

`SW1#show port-security | include err` # This command will just show you the err-disabled ports in the port security table.

### How to clear port-security

`SW1#clear port-security all` # This command will clear any port-security violations.

`SW1(config-if)#shut`
`SW1(config-if)#no shut` # These two commands reset the interface. This is how you clear the **"err-disabled"** state on an interface.