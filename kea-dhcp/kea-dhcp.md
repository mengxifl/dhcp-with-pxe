# kea-dhcp

Why Choose Kea?
https://www.isc.org/kea/

The doc is here
https://kea.readthedocs.io/en/kea-2.6.1/

Here I only use the basic features. However, some parameters require changes, so I wrote a script to handle this.

All require 

```bash
#!/bin/bash


LISTEN_INTERFACE="INTERFACE_NAME"
# You can use the command [ip addr show] to display all interface names

NEXT_SERVER_IP='192.168.1.100'
# The 'next server' IP is typically set to point to the TFTP server

ASSIGN_NET_STATMENT='192.168.1.50 - 192.168.1.70'
# assign to client statment

DHCP_SUBNET='192.168.1.0/24'
# will assign to client net mask to 255.255.255.0

ASSIGN_GATEWAY='192.168.1.1'
# gateway

NAME_SERVER='8.8.8.8, 8.8.4.4'
# nameserver or dns server

iPXE_NET_BOOT_FILE='http://<ServerIP>:<ServerPort>/<path>/<netBootFile>'
# ipxe file url

UEFI32_BOOT_FILE='ipxe-i386.efi'
# UEFI32 bios use file

UEFI64_BOOT_FILE='ipxe-x86_64.efi'
# UEFI64 bios use file

LEGACY_BOOT_FILE='undionly.kpxe'
# LEGACY bios use file
```

