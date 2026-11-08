---
title: Frequently Asked Questions (FAQ)
---

### What is Droidian?
 Droidian is a GNU/Linux distribution based on top of Debian with Mobian repositories on top providing a Debian-based distribution for mobile devices. The goal of Droidian is to be able to run Debian on Android phones.This is accomplished by using well-known technologies such as libhybris and [Halium](https://halium.org/).

### What is Halium?
 Halium is the collaborative project to unify the Hardware Abstraction Layer for projects which run GNU/Linux on mobile devices with pre- installed Android.

### How different is Droidian from Mobian ? Aren't they same?
 Droidian uses the Halium container in combination with libhybris to use Android drivers in a Linux userspace. On the other hand, Mobian uses fully open source drivers and a mainline kernel to achieve the same outcome

### What makes Droidian different from Ubuntu touch ?
 Droidian uses Debian as a base and It can be treated as a desktop operating system modified to run on Android devices.
 While Ubuntu Touch is built as a GNU/Linux operating system with user friendliness in mind.

### Which device is the best to give Droidian a try? 
Have a look at the list of [officially supported devices](https://devices.droidian.org/devices/).

### Can i run Droidian on my phone?
 The list of devices that can run Droidian and the instruction to install them can be found at [devices.droidian.org](https://devices.droidian.org/)

### My device is not listed at devices.droidian.org. What should i do now?
You can follow the porting guide available [here](https://github.com/droidian/porting-guide)

### Can an Ubuntu touch devices run Droidian?
 Droidian based on Debian and utilizes Halium to interact Android devices, since Ubuntu touch also utilizes Halium, if a device has been ported to Ubuntu Touch using Halium 9 or 10 or 11, it is likely that it can run Droidian without the need to change anything in the kernel provided by UBports.

### Why does Droidian use the Android kernel? Why not mainline linux kernel?
We rely on the Android Linux kernel and drivers to make all of the functionality provided by Android drivers work.

### Can I run Android applications in Droidian?
Yes, Waydroid can provide a pretty much complete Android experience. Use [this](https://github.com/droidian/droidian/wiki/Android-app-support) tutorial to install it.

### Can I run Flatpak applications on Droidian?
Yes. The install instructions can be found [here](https://flatpak.org/setup/Debian)

### Can I run KDE or Plasma Mobile?
No

### Can I run Gnome or SXMO?
No

### How to resize the rootfs?
for instructions refer the [link](https://github.com/droidian/droidian/wiki/Some-useful-tips-and-scripts#how-to-resize-the-rootfs)

### How to connect via SSH?
for instructions refer the [link](https://github.com/droidian/droidian/wiki/Some-useful-tips-and-scripts#how-to-connect-via-ssh)

### How to change password/PIN?
 Password can be changed in the settings app the minimum number of characters being 6.

### How to disable keyboard vibration (haptics)?
gsettings set org.sigxcpu.feedbackd.application:/org/sigxcpu/feedbackd/application/sm-puri-squeekboard/ profile silent



