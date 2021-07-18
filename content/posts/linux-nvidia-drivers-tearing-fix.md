+++
date = "2021-07-17T08:21:55Z"
title = "Fix for screen tearing on linux using NVIDIA drivers"
description = "Nailing down annoying issue with drivers => 364.12"
tags = ["things", "games", "linux", "nvidia"]
categories = ["things", "games"]
cover = ""
+++

Sometimes when using proprietary NVIDIA drivers on linux machine you can experience [something like this](https://en.wikipedia.org/wiki/Screen_tearing).
Unfortunately this is a very common issue on laptops with hybrid graphics using [NVIDIA Optimus](https://en.wikipedia.org/wiki/Nvidia_Optimus).
To address this the trick called [PRIME Synchronization was introduced back in 2016](https://forums.developer.nvidia.com/t/prime-and-prime-synchronization/), it works well but to be able to use it linux users often need to enable it manually.

# Solution
**Make sure that you using drivers ```>=364.12```**

Add ```nvidia-drm.modeset=1``` parameter to ```GRUB_CMDLINE_LINUX_DEFAULT``` line in ```/etc/default/grub``` file.

So it's gonna look like this:
```c
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nvidia-drm.modeset=1"
```
Update GRUB bootloader:
```sh
update-grub
```
Restart your machine

# Links
* [Arch Wiki: Kernel mode setting](https://wiki.archlinux.org/title/Kernel_mode_setting)
* [Arch Wiki: NVIDIA DRM kernel mode setting](https://wiki.archlinux.org/title/NVIDIA#DRM_kernel_mode_setting)