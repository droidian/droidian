---
title: Choosing GUI
---

The default graphical user interface in Droidian is [Phosh](https://phosh.mobi/). Alternatively, experimental packages are available that allow to install and use [Plasma Mobile](https://plasma-mobile.org/). 

These graphical shells rely on different software stack under the hood, and provide both different user experience and different default choice of apps.

## Choosing Phosh

[Phosh](https://phosh.mobi/) is the default GUI for Droidian, and therefore it is well tested and contains more bugfixes related  to the Droidian adaptation. It is a recommended choice for new users. 

* Phosh is available for all supported phones, both for the **current** and **next** [versions](Droidian-versions). Images based on phosh have can be easily guessed by the image file name, for example:

    > droidian-OFFICIAL-**phosh**-phone-volla_mimameid-api32-arm64-101.20251130_20251207.zip

* If you are running Droidian with a different GUI (Plasma Mobile), you still can revert to Phosh just by installing its packages:

    ```bash
    sudo apt install droidian-phosh-full
    sudo apt purge plasma-mobile* droidian-quirks-plamo-wf
    ```

**WARNING:** It is much safer to switch GUI with `apt` when you [have working SSH connection set up](https://github.com/droidian/droidian/wiki/Some-useful-tips-and-scripts#how-to-connect-via-ssh) - just in case your previous GUI becomes non-responding during the switch, or if the switch goes wrong due to some existing customizations, causing Phosh malfunction after the reboot.
{: .notice--warning}

Also, it would be a wise choice to backup all valuable data and configuration files before switching the GUI. 

**NOTE:** When you are reverting to Phosh after trying Plasma Mobile, you may also be interested in removing apps which were automatically installed with the switch. In this case, check the apt history, `/var/log/apt/history.log`, for the names of the appropriate packages.
{: .notice--info}

## Choosing Plasma mobile

[Plasma Mobile](https://plasma-mobile.org/) GUI has experimental status in Droidian, which means that it may have (and highly probably has!) bugs, and is generally less polished from the Droidian adaptation point of view.

* Pre-built flashable Plasma Mobile images are available for *some* supported phones, both for the **current** and **next** [versions](Droidian-versions). Images based on plasma-mobile mention `plamo-wf-experimental` in the image file name, for example:

    > droidian-OFFICIAL-**plamo_wf_experimental**-phone-lenovo_bronco-api32-arm64-101.20251130_20251207.zip

* If you are running Droidian with Phosh, you can switch to Plasma Mobile at any time just by installing its packages (at least this works with Droidian **current** [version](Droidian-versions)):

    ```bash
    sudo apt install droidian-plamo-wf-full
    ```

**WARNING:** It is much safer to switch GUI with `apt` when you [have working SSH connection set up](https://github.com/droidian/droidian/wiki/Some-useful-tips-and scripts#how-to-connect-via-ssh) - just in case your previous GUI becomes non-responding during the switch, or Plasma Mobile will not operate properly after the reboot.
{: .notice--warning}

Also, it would be a wise choice to back up all valuable data and configuration files before switching the GUI. 

## Screen gestures

Both **Phosh** and **Plasma Mobile** heavily rely on touch gestures. 

Plasma Mobile runs on top of the **Wayfire** Wayland compositor, while Phosh GUI uses a **Phoc** Wayland compositor created specifically for the Gnome ecosystem. Except providing accelerated graphics and windows effects, compositor also handles screen gestures, and there comes a noticeable difference between Phoc and Wayfire in this regard. 

### Gestures in Phosh

Core gestures in **Phoc/Phosh** (swiping up to close, swiping down to show quick settings bar, etc.) are hardcoded in the shell+compositor combo and not supposed to be reconfigured. Adding new user-configured gestures is theoretically possible via third-party userspace tools, such as [Touchégg](https://github.com/JoseExposito/touchegg) daemon, but that's no way a mainstream thing to do.

### Gestures in Plasma Mobile

Gestures in **Wayfire** (like edge swipe from the right to show all running apps and then swipe to close the needed app, etc.) are much more independent from Plasma Mobile and can be flexibly configured (each of 4 screen edges is split in 3 sections, each of which can trigger different actions). This independence of gesture navigation from Plasma Mobile GUI can be considered an advantage, taking into account the fact that Plasma has experimental status and may not work as intended in some parts due to not yet fixed or newly emerged bugs. 

Gestures are set up in the Wayfire configuration file, `/home/droidian/.config/plasma-mobile-wf/wayfire.ini`. See contents of this file for the current configuration, and the [official Wayfire documentation](https://github.com/WayfireWM/wayfire/wiki/Configuration) for details.
