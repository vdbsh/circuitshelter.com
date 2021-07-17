+++
date = "2021-07-17T04:20:16Z"
title = "Using BIND 9 RPZ as DNS firewall"
description = "Filtering DNS requests with BIND 9 and Response Policy Zone"
tags = ["servers"]
cover = ""
+++

[DNS Response Policy Zones (RPZ)](https://kb.isc.org/docs/aa-00525) is an open and vendor-neutral standard for the interchange of DNS firewall configuration information. It is a standard feature of [BIND 9](https://www.isc.org/bind/), and is expected to be supported by other (non-BIND) name servers. Using it we can easily build something like [Pi-hole](https://pi-hole.net/).

# RPZ file generation
Let's generate RPZ file with hosts we want to filter using [HOSTS from StevenBlack](https://github.com/StevenBlack/hosts) and [Python](https://www.python.org/).

```python
#!/usr/bin/env python3

from urllib import request
    
rpz_file         = 'rpz-filter.db'
hosts_file_url   = 'https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts'

comment_char  = '#'
local         = ('127.0.0.1', '255.255.255.255', '::1', 'f')
default_route = '0.0.0.0'

zone_header = """$TTL 2w
@ IN SOA localhost. root.localhost. (
       2   ; serial 
       2w  ; refresh 
       2w  ; retry 
       2w  ; expiry 
       2w) ; minimum 
    IN NS localhost.

"""

def generate_rpz_file():
    hosts = 0
    file = open(rpz_file, 'w')
    file.write(zone_header)

    with request.urlopen(hosts_file_url) as f:
        for bytes in f:
            line = bytes.decode('utf-8').strip()
            if (not line or line.startswith(comment_char) or line.startswith(local)):
                continue

            domain = line[8:].split(' ')[0]
            
            if domain == default_route:
                continue

            file.write(f'{domain} CNAME .\n')
            file.write(f'*.{domain} CNAME .\n')
            hosts += 1

    file.close()
    print(f'Total hosts in filter: {hosts}')

if __name__ == '__main__':
    generate_rpz_file()
```


# Configuration
RPZ zone files can be added to ```named.conf.options``` as:
```c
zone "rpz-filter" { type master; file "/etc/bind/rpz-filter.db"; };
options {
    response-policy { zone "rpz-filter"; };
};
```
Reload zone files and configuration changes:

```
service bind9 reload
```

# Links
[BIND 9 Configuration Reference](https://bind9.readthedocs.io/en/latest/reference.html)