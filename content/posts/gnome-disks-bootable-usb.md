+++
date = "2021-07-19T21:01:43Z"
title = "Creating bootable USB drives with GNOME Disks"
description = "No additional tools required"
tags = ["things", "linux", "gnome"]
categories = ["things"]
cover = ""
+++

Just launch GNOME Disks:
```sh
gnome-disk-utility
```

```Select your thumb drive -> [context menu] -> Restore Disk Image... -> Select your ISO```

# Notes
This is not gonna work with anything that require complex partitioning like Windows 10,
but will do for the vast majority of linux distributions which booting fine just from single UDF partition.