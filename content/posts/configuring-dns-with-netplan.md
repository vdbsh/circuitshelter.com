+++
date="2021-08-06T18:21:03Z"
title="Configuring DNS setting for Ubuntu with Netplan"
description="Works with Ubuntu 18.04+"
categories=["servers"]
tags=["servers", "linux"]
cover=""
+++

Since 18.04 Ubuntu uses [systemd-resolved](https://manpages.ubuntu.com/manpages/en/man8/systemd-resolved.service.8.html) for name resolution and setting DNS in /etc/resolv.conf will no longer work.
Now to set such things we need to make changes to [Netplan](https://netplan.io/) [configuration](https://netplan.io/examples/) which delegates name resolution to systemd-resolved.resolv.conf.

```sh
vim /etc/netplan/my-dns-config.yaml
```

Assuming we are gonna set [public Cloudflare DNS](https://www.cloudflare.com/learning/dns/what-is-1.1.1.1/) for both IPv4 and IPv6 for interface ```ens3```:

```yaml
# This is my DNS config
network:
  ethernets:
    ens3:
      dhcp4: true
      dhcp4-overrides:
        use-dns: false
      nameservers:
        addresses: [1.1.1.1, 1.0.0.1, 2606:4700:4700::1111, 2606:4700:4700::1001]
  version: 2
```

Test configuration before apply:
```sh
netplan --debug apply
```

Apply:
```sh
netplan apply
```

Check DNS settings with systemd-resolved:
```sh
systemd-resolve --status
```