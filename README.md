# OpenWRTAgent
 Agent program for remotely managing OpenWRT AP
-------------
## Introduction
#### This project includes an agent program for remotely managing OpenWRT.

## Requirements
#### Raspberry Pi B2 OpenWRT + ipTIME N100UM Wireless LAN card

## OpenWRT Package Installation
* Install OpenWRT package for setting up wireless LAN
`$ opkg install kmod-cfg80211 kmod-mac80211`
* Install USB driver package for wireless LAN recognition
`$ opkg install kmod-rt2800-lib kmod-rt2800-usb kmod-rt2x00-lib kmod-rt2x00-usb`
* Install OpenWRT package for Uplink/Downlink bandwidth control
`$ opkg install wshaper`
* Install OpenWRT package for bandwidth monitoring
`$ opkg install iftop`

## OpenWRT Network Configuration
#### Setting for AP WLAN
 ```
 $ vi /etc/config/network
 ...
 config interface 'lan'
 		option type 'bridge'
        option_orig_ifname 'eth0 wlan0'
        option_orig_bridge 'true'
        option ifname 'eth0'
        option proto 'dhcp'
        ...
 config interface 'wifi'
 		option proto 'static'
        option netmask '255.255.255.0'
        option ipaddr '192.168.222.1'
        
 ```
  
 ```
 $ vi /etc/config/wireless
 ...
 config wifi device 'wlan0'
 		option type 'mac80211'
        option hwmode '11g'
        option path 'platform/bcm2708_usb/usb/1-1/1-1.2/1-1.2:1.0'
        option htmode 'HT20'
        option country '00'
        option txpower '20'
        option channel '11'
        ...
 config wifi-iface
 		option device 'wlan0'
        option mode 'ap'
        option encryption 'psk'
        option network 'wifi'
        option key 'openwinnet'
        option ssid 'openwinnet'
 ```
 
 
 ```
 $vi /etc/config/dhcp
 ...
 config dhcp 'wifi'
 		option interface 'wifi'
        option start '100'
        option limit '150'
        option lease time '12h'
        ...
 ```
 
 ## Compile
 `$ make clean`
`$ make ow_agent`
`./ow_agent`

 
