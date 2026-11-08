---
title: Android app support (Waydroid)
---

Waydroid is a container-based approach to boot a full Android system on a regular GNU/Linux system.

To install Waydroid, run the following in your command line:

```
# apt update
# apt install waydroid
```

## Waydroid with GAPPS

If you really want them, Waydroid can support Google services:

```
sudo rm -f /etc/apt/preferences.d/waydroid-system
sudo apt install waydroid waydroid-{system,vendor}-custom
sudo waydroid init -f -s GAPPS
```

**WARNING:** Beware that this will delete your pre-existing Waydroid images if you had installed before already. You may want to use `mv` to move the images instead of deleting them with `rm`.
{: .notice--warning}
