# Key Chains

### Authentication is a very important security measure on our enterprises. Control plane protocols like NTP, OSPF, and EIGRP will use authentication controls to verify protocols connect to a non-malicious device. In the case of protocols like NTP, EIGRP and OSPF we can use "key-chains" to create Pre-Shared Keys globally on our device that we can use to authenticate between protocols/devices.

### We can use key-chains to authenticate between our routing protocols, and we can rotate keys by implementing time based restrictions our on PSKs, in our key-chain.

### - In this How To we will configure a key-chain with different keys and different **"lifetime"** for the keys. This will demonstrate how we can **"roll"** keys.

![](/Key%20Chains/key_chain_network_diagrams.png)

`SW1(config)#key chain DEMO` # This command will create the key chain and bring you into the **"Key Chain"** sub-configuration mode

`SW1(config-keychain)#key 1` This command creates an actual key to be used to authenticate. this is creating the PSK, but is not the actuall **"Key"** or **"password"** that will be used.

`SW1(config-keychain-key)#key-string [password]` # This command will set the actual password to be used for authentication.

`SW1(config-keychain-key)#send-lifetime 00:00:00 1 Mar 2022 00:00:00 1 Sep 2022` # This command will set the length of time the key can be sent.

`SW1(config-keychain-key)#accept-lifetime 00:00:00 1 Mar 2022 00:00:00 1 Sep 2022` # This command will set the length of time a key can be accepted

### Full configuration is shown below

![](/Key%20Chains/key_chain_config.png)

### Verification

`SW1#show key chain` # This command will show you all the globally configured key chains and there configurations.