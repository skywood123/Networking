![image](https://github.com/user-attachments/assets/0b0ed3eb-f921-4b04-956f-bd846bdde4dd)# This lab is exploring captive portal on the gateway. The AP is just for advertising open ssid without pointing to captive portal.

The network topology as below.
![image](https://github.com/user-attachments/assets/b3bb92d9-ba1f-42b8-829b-ed2605808917)

Originally, OPNSENSE is the gateway of the network, nat the private network to the public network.

This lab setup in the environment without changing the original traffic flow.

By introducing openWRT into the network, new VLAN is created.(example: VLAN 2081)

Open SSID --- openWRT(gateway of the new VLAN) -- OPNSENSE -- Internet.

## Software versions used in this lab
1. ESXI 7
2. OpenWRT 23.05
3. Aruba VMC 8.10


# Lab setup

## Step 1 : Prepare the Open SSID
1. Create Open SSID.
2. Place user into the new VLAN 2081.
3. If using Aruba controller, change the initial role to **authenticated** , because the default logon role is restricted to DNS and ICMP services only.

## Step 2 Prepare the openWRT VM
1. Download target openWRT firmware version from [openWRT](https://firmware-selector.openwrt.org/?version=23.05.5&target=x86%2F64&id=generic) and unzip it.
2. Download qemu-img tools [here](https://cloudbase.it/qemu-img-windows/)
3. The downloaded openWRT firmware is in .img format. We need to convert it to vmdk to be used by ESXI VM.
4. ```qemu-img convert -f raw -O vmdk openwrt-x86-generic-combined-ext4.img openwrt-x86-generic-combined-ext4.vmdk```
5. Upload to your ESXI machine storage.
6. Create VM in ESXI.
7. Choose the uploaded VMDK as disk1 (else it wont boot up).
 ![image](https://github.com/user-attachments/assets/23ea494d-f03c-479e-8302-507d3bf1bf11)
![image](https://github.com/user-attachments/assets/b2e7f694-8262-4f8a-b1ed-8856027b4036)
8. Configure the network adapter. One for WAN, one for LAN. In my lab, network adapter 2 is mapped to the WAN, network adapter 1 is mapped to the br-int, the LAN.
9. ![image](https://github.com/user-attachments/assets/c2f4d2d4-f168-4f81-8c1e-712b9d82c02c)
10. Boot up the VM and access from ESXI.
11. Initially, openWRT web GUI Luci is only listening at the LAN. You can assign a temporary IP address to the LAN.
12. ``` ip address add 172.99.0.1/20 dev br-int```
13. Access the openWRT GUI from the new VLAN.
## Step 3 Configure openWRT 
1. Configure the ip addresses for the LAN and WAN in the openWRT gui.
2. ![image](https://github.com/user-attachments/assets/6841883a-67d5-4c5c-820f-73dbf17b3b45)
3. You can assign firewall rule, to allow gui access from WAN interface.
4. By default traffic is allowed from LAN to WAN.
## Step 4 Installing opennds
1. Go to **System > Softwares** , update the package lists
2. Install the opennds package
3. ![image](https://github.com/user-attachments/assets/71790ca1-294c-44ce-bc6e-2a5bdf0dfcd4)
4. By default, opennds will redirect user to captive portal from interface br-int. Make sure the service is running. If the service crashed/stopped, error occured in the backend.
5. ![image](https://github.com/user-attachments/assets/cd677406-6b46-4ef9-9c08-f29ab10201b1)

## Verification
1. Connect to the open SSID, captive portal is pop up.
2. ![WhatsApp Image 2025-01-06 at 14 24 59_ef359b4a](https://github.com/user-attachments/assets/8835d626-ccee-4970-9276-c2dc51690760)









