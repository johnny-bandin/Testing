# DHCP Configuration 

### In this How To we will cover creating a DHCP pool on Cisco iOS, the different options typically configured in an enterprise, DHCP exclusions, and DHCP VRF configuration, and the configuration of a DHCP relay.

![](dhcp_network_diagram.png)

- First we must configure the VLANs, assign the correct ports to the VLANs, and create the SVIs. It assumed that you already know how to do this. If not please refer to the **VLANs** How To's.

- Next comes the actual DHCP iOS Configuration

`SW1(config)ip dhcp pool [NAME]` # This command will create the DHCP pool.

`SW1(config-dhcp)#network [network address][CIDR]` # This command sets the network address in the pool

`SW1(config-dhcp)#default-router [DG IP Address]` # This command sets the default gateway in the pool

`SW1(config-dhcp)dns-server [Primary DNS IP][Secondary DNS IP]` # This command sets the DNS server IP addresses to be allocated in the pool

### This is the basic configuration of a DHCP pool in Cisco iOS to get the pool up and running. Shown below is the full configuration for both DHCP pools in our diagram

![](dhcp_basic_config.png)

### - Now lets go over configuring the lease time and the commonly used **"options"** configured in a DHCP pool.

`SW1(config-dhcp)#lease 7` # This command sets a time for how long an IP address can assigned to an endpoint before being released back into the DHCP pool

`SW1(config-dhcp)#option 150 ip [Primary CUCM IP] [Secondary CUCM IP]` # This command sets the IP addresses for the Cisco Unified Call Managers. These are the servers that deliver a phones configuration via TFTP.

`SW1(config-dhcp)$option 66 ip [WDS|PXE IP address]` # This command sets the IP address for a Windows Deployment Server which is needed for  the Pre-execution Environment which allows re-imaging of computers over the LAN/Wire.

### - Shown below is the full configuration of these options.

![](dhcp_options_config.png)

### - Now lets go over exclusions. It is sometimes needed to exclude IP addresses from the DHCP pool to be assigned. In this example we will exclude the printer's IP address.

`SW1(config)#ip dhcp excluded-address [IP Address | X.X.X.X]` # This command will exclude an IP address from being assigned to a user.

`SW1(config)#ip dhcp excluded-address 10.10.10.50 10.10.10.60` # This command sets a range of IP addresses to be excluded from being assigned to an endpoint device.

### Shown below is the full configuration.

![](dhcp_exclusion.png)

### - Now we are going to go over VRF support for DHCP and how to assign a DHCP pool to a VRF's Subnet. We will be covering VRF's in a later section

`SW1(config)#ip dhcp pool [NAME]` # This command will create the DHCP pool.

`SW1(config-dhcp)#vrf [NAME]` # This command will set the DHCP pool to be apart of the VRF

### The full configuration is shown below.

![](vrf_dhcp.png)

# Now we will cover configuring a DHCP relay with the IP Helper-address command. The ip helper-address command will need to be configured under each interface that has a subnet and users that will need IP addressing from the DHCP server. 

![](dhcp_relay_network_diagram.png)

### Now lets go over the actual configuration

`SW1(config)#interface vlan 10` # This command creates an SVI on the switch

`SW1(config-if)#ip helper-address [ip address X.X.X.X]` # This command will now redirect any broadcast traffic destined to the ip address that we have configured

### Shown below is the full configuration 

![](dhcp_relay_config.png)


# Verification

### Now we will go over the show commands used to troubleshoot and help manage DHCP pools on Cisco iOS

`SW1#show ip dhcp pool` # This command will show the current DHCP pools configured on your Cisco iOS device, the amount of available IP addresses in the pool, and the currently leased addresses.

![](show_ip_dhcp_pool.png)

`SW1#show ip dhcp binding` # This command will show all the current IP addresses assigned to devices, the MAC addresses of devices, and the lease times.

![](show_ip_dhcp_binding.png)

`SW1#show ip dhcp vrf [name] binding *` # This command will show all the DHCP bindings under a VRF

`SW1#show ip dhcp conflicts` # This command will show if any devices are trying to pull the same IP address from a DHCP pool

`SW1#clear ip dhcp binding [ * | X.X.X.X | vrf]` # This command will clear DHCP bindings. There are a few options you put on this command. Clear all bindings with an *. Clear one binding by specifying an IP address. And clear bindings under a VRF.

`SW1#clear ip dhcp conflicts [ * | X.X.X.X | vrf]` # This command will clear DHCP conflicts. There are a few options you put on this command. Clear all conflicts with an *. Clear one conflict by specifying an IP address. And clear conflicts under a VRF.

### In the photo shown below we can see a Wireshark/TCP capture of the DORA process from endpoint to Cisco iOS device.

![](wireshark_capture.png)

### In this capture you intitially see the discover is sent with a source address of 0.0.0.0 because the device does not have an IP address. Then after the DHCPack we see the device now has an IP address. In the video's accompinying these How To's we will take a deep dive into each DHCP packet in DORA.


