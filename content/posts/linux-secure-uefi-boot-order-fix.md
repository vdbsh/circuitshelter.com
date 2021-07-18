+++
date = "2021-07-17T11:40:56Z"
title = "Fixing Secure Boot Violation on linux"
description = "How-to correct UEFI boot order"
tags = ["servers", "linux"]
categories = ["things"]
cover = ""
+++

On the linux machines with enabled Secure Boot you can catch something like this:
```
---------------------Secure Boot Violation---------------------
|Invalid signature detected. Check Secure Boot Policy in Setup|
|-------------------------------------------------------------|
|                          [  OK  ]                           |
---------------------------------------------------------------
```

There can be different reasons for this to happen. But if this occurs right after bootloader re-build (e.x after Kernel upgrades) most likely your UEFI boot order is messed up.

# Solution
Check your boot order by:
```sh
efibootmgr -v
```

Assuming that you only want to run single OS e.x Ubuntu, wrong sequence can look like:
```
BootCurrent: 0000
Timeout: 0 seconds
BootOrder: 0003,0002,0000,0001
Boot0000* ubuntu
Boot0001* CDROM
Boot0002* NIC
Boot0003* ubuntu
```
In this example Ubuntu tries to boot with the unsigned boot loader - which of course does not work.
We need to change the default boot loader from grubx64.efi to shimx64.efi,
so the right sequence will be: ```0000, 0003, 0001, 0002```.

We can set it directly in BIOS/UEFI or with ```efibootmgr```:
```sh
efibootmgr -o 0000,0003,0001,0002
```

Reboot the machine to test changes.

# Links
* [How UEFI Secure Boot works on Ubuntu](https://wiki.ubuntu.com/UEFI/SecureBoot#How_UEFI_Secure_Boot_works_on_Ubuntu)
* [MAN efibootmgr](https://manpages.ubuntu.com/manpages/focal/man8/efibootmgr.8.html)