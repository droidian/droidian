---
title: Droidian versions
---

Being based on Debian, Droidian follows it's rolling release scheme with stable and testing versions of the distro. Each time there is a stable version called **current**, and an unstable/testing version called **next**. These versions also have predictable numbering: for example, if the current stable version of Droidian is **101**, then the version under testing would be **102**. The **current**'s version number is mentioned in the name of [Droidian release](https://github.com/droidian-images/droidian/releases) – something like [Droidian 101 (patchlevel 2025-11-30)](https://github.com/droidian-images/droidian/releases/tag/droidian%2F101.20251130), as well as in the appropriate image names). 

During the development, the **next** version of Droidian will be declared as as stable with the appropriate version numbers increment. In context of the previous example, **current** should become **102**, while the new **next** version should probably get version number **103**.

## The "current" (stable version)

The **current** Droidian version generally follows approach of the **stable** Debian release channel.

**Current** version is good choice for phones used as a daily driver. For example, when the reliable functioning and non-broken basic functionality like cellular calls and fault-less GUI are in demand, **current** is a recommended variant. Also it is highly recommended for users with a limited experience in GNU/Linux phones.

The **current** version images for all supported phones are available under the **Assets** section [in all stable/numbered Droidian releases](https://github.com/droidian-images/droidian/releases).

Packages updates for **current** release channel come not too often; they may cover security issues and some bug fixes, but stick to the software versions frozen when the previous "next" had turned into "current".

## The "next" (development version)

The **next** version mimics the Debian Unstable version (the one which always has the codename "Sid"). If follows the rolling release model, which means packages are updated all the time (and the same is true for bugs and bugfixes). 

The **next** Droidian version can be recommended for advanced users capable of tweaking their mobile Linux installation, as well as reporting bugs and testing bug fixes.

Also, the **next** is a considerable choice for users who don't have stability in their priority list, and need some recently added functionality without waiting when it finally get into **current**.

The latest **next** images can be found under the **Assets** section [in the Nightly builds](https://github.com/droidian-images/droidian/releases/tag/nightly) (pre-release) part of the Droidian releases page.

## Version switching

Flashing the appropriate image is the obvious way to switch from **current** to **next** and back, and it is normally more error-prone. Still, the version switch on the go (without reflashing) is also possible.

You will need to [setup SSH access to your phone](https://github.com/droidian/droidian/wiki/Some-useful-tips-and-scripts#how-to-connect-via-ssh) to switch versions on the go.

**WARNING:** Back up all valuable data from your home directory and configuration files before proceeding. This will allow you to restore your environment and data if the image reflashing will be needed because of something went wrong.
{: .notice--warning}

Dynamic version switching requires the following steps:

1. Connect to your phone via SSH. You will immediately see Droidian's command prompt in your terminal, something like

    ```bash
    droidian@MyPhone:~$
    ```
    Next operations of the current instruction will be done from your computer via this SSH session.

2. Create a file `/etc/apt/apt.conf.d/90-droidian-snapshot`, if it does not exist.

    Open it under `sudo` with your text editor and put in it the following line:

    * If you are switching to the **current** version:

        ```
        Acquire::Droidian::Version "current";
        ```

    * If you are switching to the **next** version:

        ```
        Acquire::Droidian::Version "next";
        ```
3. Run the following commands:

    ```bash
    sudo rm -rf /var/lib/apt/lists/*
    sudo apt update
    sudo apt dist-upgrade
    ```
4. Reboot the phone to see the Droidian version of your choice alive.
