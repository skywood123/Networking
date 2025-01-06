# This lab is exploring captive portal on the gateway. The AP is just for advertising open ssid without pointing to captive portal.

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

## Step 2 Prepare the openWRT
1. Download target openWRT firmware version from openWRT(https://firmware-selector.openwrt.org/?version=23.05.5&target=x86%2F64&id=generic) and unzip it.
2. Download qemu-img tools here(https://cloudbase.it/qemu-img-windows/)
3. The downloaded openWRT firmware is in .img format. We need to convert it to vmdk to be used by ESXI VM.
4. """qemu-img convert -f raw -O vmdk openwrt-x86-generic-combined-ext4.img openwrt-x86-generic-combined-ext4.vmdk"""
5. Upload to your ESXI machine storage.
6. Create VM in ESXI.
7. Choose the uploaded VMDK as disk1 (else it wont boot up).
 


