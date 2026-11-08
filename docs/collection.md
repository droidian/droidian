---
title: A collection of information
---

Here is a bunch of information provided by the community to ease the usage of Droidian for the end user

Visit [devices.droidian.org](https://devices.droidian.org/) for information about installation.

## Unlocked phone

To use an other OS/ROM than the default OS of the smartphone, the smartphone must be unlocked. Be aware, in some case the warranty will be loosed.

### Unlock OnePlus

Enable OEM unlock and USB debugging
Boot to fastboot

```
fastboot oem unlock
```

### Unlock Sony

See [this]{https://developer.sony.com/develop/open-devices/get-started/unlock-bootloader#unlock-code).

### Unlock Xiaomi

It is not an easy operation. It is necessary to have:

* an account in the Xiaomi's website;
* a SIM card with the ability to use Internet;
* a Windows to use the Xiaomi's tools associated with the navigator and the connection with the account on the Xiaomi's website. 

### Unlock Samsung

For modern Samsung phones:

Usually the following method :-

* Settings -> About phone -> click a couple of time on build number to enable Developer options (Enter pattern/password if prompted to)
* Settings -> Developer options -> Enable OEM unlocking
* Power off the phone
* Connect USB into PC and Phone
* Hold Volume Up + Volume Down
* A blue screen should appear with few options
* (WARNING, This will ERASE all your data), Long press on Volume Up should take you to unlock mode

For older phones (which Droidian will *probably* not work with anyways, but you can try if you have Halium or stuff)

* Just do a quick search on "How to unlock bootloader of (Device Name/CODENAME)"

# Installation tips (04-23-2022)

## Resize 'rootfs.img'

To resize rootfs, boot TWRP and type the following commands:

```
# e2fsck -f /data/rootfs.img
# resize2fs /data/rootfs.img 16G
```

Resizing is not needed for official devices.

## Hotspot network

Hotspot networks don't have access to mobile data as no routing is done. to fix this iptables can be configured to route the data.
Run these commands line by line

`sudo sysctl net.ipv4.ip_forward=1`

`sudo iptables -t nat -A POSTROUTING -o rmnet_data0 -j MASQUERADE`

`sudo iptables -A FORWARD -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT`

`sudo iptables -A FORWARD -i wlan0 -o rmnet_data0 -j ACCEPT`

Check the interface `rmnet_data`. it might be `0`, or `1`, or another number.

A warning was given about a possible problem for TWRP to backup a big 'rootfs' image.

## Choose the slot '0' or '1' - Eugenio 06-18-2022

you can always access android's bootctl on Droidian side so that you can switch slots (something like sudo android_bootctl set-current-slot 0/1).

on Android you probably need root to switch those.

# Configuration tips (11-07-2022)

## The Mobian Wiki

Most of Mobian's tweaks also apply to Droidian: [Tweaks & Customizations](https://wiki.mobian.org/doku.php?id=tweaks)

## How to change the scale

Phosh scaling can be changed using the following guide: [Phosh scaling](https://github.com/droidian/porting-guide/blob/master/debugging-tips.md#phosh-scaling). 

Create /etc/phosh/phoc.ini and change the following:

> [output:HWCOMPOSER-1]
> scale = 2 

You can set `scale` at the value that you prefer.

## Phosh configuration

The default Phosh configuration can be inspected at `/usr/share/phosh/phoc.ini`

## Squeekboard Keyboard modify/tab key

you can modify the keyboard by yourself, following will just add tab key to first page

```
mkdir -p ~/.local/share/squeekboard/keyboards/terminal/
cd ~/.local/share/squeekboard/keyboards/terminal/
wget https://gist.githubusercontent.com/magdesign/33aa088987d0df044eb75e5a263ca76d/raw/03bd5b07096293be649f88c10cd7e475e5ee1c63/us.yaml
```

If you need umlauts [use this](https://gist.githubusercontent.com/Peetz0r/3cf7d6f8cff6b64f542716fbfd878423/raw/6418ff9fb346aebfe859786b4a9e953e335419dc/terminal.yaml).


## Porting guide

Refer to the porting guide to learn to compile and build Droidian for a device.

The porting guide can be viewed [here](/docs/porting/)

## GSI

GSI images (as in the Android sense) must work otherwise your device wouldn't get google's certification, The Halium image Droidian ships is in fact a stripped-down Android GSI, that's why you don't have to build that manually

## Backup an encrypted partition (Eugenio / 2022-07-11).

`ssh root@192.168.2.15 "dd if=/dev/mapper/droidian_encrypted | gzip -c" | dd of=bk.img.gz status=progress`

# Software quirks, fixes and tips

## Telegram Desktop (and perhaps any Qt software): compose and dead keys not recognized

If you use a keyboard layout with dead keys like en_US intl with dead keys, or any layout with compose key enabled, you'll see that `telegram-desktop` just ignores it, and perhaps all Qt applications show the same issue. They fail to read from the Compose file shipped with the system and need it in your `$HOME`. Running this should fix the issue: `ln -s /usr/share/X11/locale/en_US.UTF-8/Compose ~/.XCompose` ([source](https://github.com/telegramdesktop/tdesktop/issues/1041#issuecomment-1315722659)).

## Foot: compose and dead keys not recognized

You may need to set the `LC_CTYPE` environment variable to one supporting compose and dead keys: `LC_CTYPE="en_US.utf8" foot -c $HOME/.config/foot/foot.ini`.

It is recommended to add the `--server` argument to that command and autostart it with Phosh (add a script in `~/.config/autostart`), so that `footclient` can be started more quickly than independent `foot` processes, and attached to the pre-loaded server. If you have a hardware keyboard, then setting a global keybinding for `footclient` in Phosh settings allows quickly spawning a new terminal window from anywhere without pulling the app launcher.

## Start Sway as a WM nested in Phosh

```
sudo apt install sway
WLR_BACKENDS=wayland sway
```
This will open a window in Phosh, containing a desktop with SwayWM. The resolution in that window will depend on your Phosh scaling factor. If Phosh is scaled to 100%, then the window will be in the native resolution of your screen; if Phosh is scale to 200%, then the resolution of the window wil be halved. If used for convergence with an external monitor, then it is recommended first setting Phosh scaling factor to 100% before starting Sway and moving the window to the external monitor.

See demo and limitations [here](https://youtu.be/WkxzsoP8BvI?t=150).

## Make **Firefox** mobile friendly

Purge the old method:

```
sudo apt purge firefox-esr-mobile-config
```

Clone user0 repo:

```
git clone https://codeberg.org/user0/Mobile-Friendly-Firefox.git
```

Make script executable:

```
chmod +x Mobile-Friendly-Firefox/install.sh
```

Run the script (make sure to select "Add Recommended Preferences" and "Hide Extension Button" and "Default Theme", otherwhise you will miss the back button):

```
./Mobile-Friendly-Firefox/install.sh
```

Restart firefox twice to get the changes applied.

