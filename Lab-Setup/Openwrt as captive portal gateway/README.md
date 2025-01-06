## This lab is exploring captive portal on the gateway. The AP is just for advertising open ssid without pointing to captive portal.

The network topology as below.
![image](https://github.com/user-attachments/assets/b3bb92d9-ba1f-42b8-829b-ed2605808917)

Originally, OPNSENSE is the gateway of the network, nat the private network to the public network.

This lab setup in the environment without changing the original traffic flow.

By introducing openWRT into the network, new VLAN is created.

Open SSID --- openWRT(gateway of the new VLAN) -- OPNSENSE -- Internet.

## software versions used in this lab
1. ESXI 7
2. OpenWRT 23.05
3. Aruba VMC 8.10

