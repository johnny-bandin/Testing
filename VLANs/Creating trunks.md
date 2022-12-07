# Creating Trunks

## In this How To we will cover how to create a static trunk between switches, and filter the VLANs across the link.

![Switching fundamentals](/VLANs/Switching%20fundamentals.png)

- We will need to creat a static trunk on **Ethernet0/3** between **SW1** and **SW2**.

## Configuration

- To create a trunk we must go into the sub-configuration mode of **ETH 0/3**

`SW1#conf t` # This command puts us in Global Config mode

`SW1(config)#interface ethernet 0/3` # This command puts us into the interface sub-configuration mode

`SW1(config-if)#switchport trunk encapsulation dot1q` # This command will set the trunk to use the IEEE **802.1q** Encapsulation standard

`SW1(config-if)#switchport mode trunk` # This command will statically set the interface to **trunkning** mode.

- The complete configuration for both switches is shown below
![sw1 trunk](/VLANs/sw1%20trunk%20configuration.png)
![sw2 trunk](/VLANs/sw2%20static%20trunk.png)

### Filtering VLANs on trunk ports

- To filter the VLANs, add or remove the VLANs allowed across a trunk we use the commands below. 

`SW1(config-if)#switchport trunk allowed vlan 1,10,20,30` # This command will only VLANs 1,10,20,30 across the trunk

`SW1(config-if)#switchport trunk allows [add | remove] vlan 40` # This command allows you to add or remove VLANs from the trunk port.

- The complete configuration is shown below
![filter vlans](/VLANs/filtering%20vlans%20on%20trunk.png)


## Verification

- The following commands will show and verify the trunks are formed, how they formed and what VLANs are allowed across the trunks.

`SW1#show interface trunk` # This command will show us the active trunks on our switch.

![show interface trunk](/VLANs/show%20interface%20trunk.png)