---
title: Some useful tips and scripts
---

The following are some of the useful tips that could help you in your Droidian journey:

## How to resize the rootfs?

To resize rootfs, boot to TWRP, open Terminal under Advanced, and type the following commands:

```
 e2fsck -f /data/rootfs.img
 resize2fs /data/rootfs.img 16G
```
This will resize the rootfs to 16 GB.

**NOTE:** the larger the rootfs, the harder it will be to make a backup from it.
{: .notice--info}

## How to connect via SSH?

Enable ssh on device:

```
sudo systemctl enable ssh
```

Then plugin via usb and:

```
ssh droidian@10.15.19.82
```
the password is `1234` by default

If no new network interface is showing up on your computer when you plug usb in, you may need to install `droidian-devtools` on the phone and restart the device.

``` 
sudo apt install droidian-devtools 
```

Additionally, if the host is Windows, and the RNDIS device in device manager shows up as broken, you may need to update the driver: browse my computer for drivers -> Let me pick from a list -> Network Adapters -> Microsoft -> USB RNDIS Adapter

## Change password

Open up the terminal app and run

```
sudo passwd droidian
```

## Hotspot has no internet

Open up the terminal app and run

```
/usr/sbin/ifconfig
```

Look for an interface with the name `rmnet_dataX` (X can be any number)

After that run

```
sudo sysctl net.ipv4.ip_forward=1
sudo iptables -t nat -A POSTROUTING -o rmnet_data0 -j MASQUERADE
sudo iptables -A FORWARD -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i wlan0 -o rmnet_data0 -j ACCEPT
```

Make sure to replace `rmnet_data0` with your interface.

## Modem not showing up (no 2G/3G/4G Signal symbol on top left)

Rebooting modemmanager might help:

```
sudo mmcli -m any -r
```

## Enable GPS

```
sudo mmcli -m any --location-enable-gps-nmea --location-enable-gps-raw
```

To make it accessable for e.g. PureMaps, start Geoclue:

```
/usr/libexec/geoclue-2.0/demos/agent 
```

## Add VPN connection from openvpn file

```
sudo nmcli connection import type openvpn file path/to/vpnfile.ovpn
```

Add the username to the connection with (replace "${vpnname}" and "${myname}" with yours:

```
nmcli connection modify "${vpnname}" +vpn.data username="${myname}"
```

Then you should be able to enable VPN via Network settings

## Screenshot with phosh

Long press the power button, then you need to paste:

```
sudo apt-get install wl-clipboard
```

```
wl-paste > ~/Pictures/Screenshots/"$(date +'%Y-%m-%d_%H:%M:%S').png"
```

## Enable desktop mode without a monitor plugged in

In `/etc/machine-info` change the value of CHASSIS from handset to desktop. now on screen keyboard can be enabled in settings->accessibility.
To go back to default change it back to handset

## Start GUI application as root

To start some GUI application as root (for example, gedit), type:

```
sudo -E gedit
```
