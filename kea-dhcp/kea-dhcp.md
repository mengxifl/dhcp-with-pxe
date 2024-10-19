# kea-dhcp

Why Choose Kea?
https://www.isc.org/kea/

The doc is here
https://kea.readthedocs.io/en/kea-2.6.1/

Here I only use the basic features. However, some parameters require changes, so I wrote a script to handle this.

You must install keadhcp first . We won't confluence there

I use container to run this server . It must add `--network=host` parms

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
# ipxe file url boot file  netboot.xyz.kpxe I will use 

UEFI32_BOOT_FILE='ipxe-i386.efi'
# UEFI32 bios use file

UEFI64_BOOT_FILE='ipxe-x86_64.efi'
# UEFI64 bios use file

LEGACY_BOOT_FILE='undionly.kpxe'
# LEGACY bios use file

CONFIG_FILE_FULL_PATH="./dhcp.json"

function updateDhcpFile {
	sed 's@VAR_LISTEN_INTERFACE@'$LISTEN_INTERFACE'@g' -i $1

	sed 's@VAR_NEXT_SERVER_IP@'$NEXT_SERVER_IP'@g' -i $1

	sed 's@VAR_ASSIGN_NET_STATMENT@'$ASSIGN_NET_STATMENT'@g' -i $1

	sed 's@VAR_DHCP_SUBNET@'$DHCP_SUBNET'@g' -i $1

	sed 's@VAR_ASSIGN_GATEWAY@'$ASSIGN_GATEWAY'@g' -i $1

	sed 's@VAR_NAME_SERVER@'$NAME_SERVER'@g' -i $1

	sed 's@VAR_iPXE_NET_BOOT_FILE@'$iPXE_NET_BOOT_FILE'@g' -i $1

	sed 's@VAR_UEFI32_BOOT_FILE@'$UEFI32_BOOT_FILE'@g' -i $1

	sed 's@VAR_UEFI64_BOOT_FILE@'$UEFI64_BOOT_FILE'@g' -i $1

	sed 's@VAR_LEGACY_BOOT_FILE@'$LEGACY_BOOT_FILE'@g' -i $1	
}


function runKeaDHCP {
	/usr/local/sbin/kea-dhcp4 -c $1
}

updateDhcpFile "$CONFIG_FILE_FULL_PATH"
runKeaDHCP "$CONFIG_FILE_FULL_PATH"
```

This is a configuration file that allows your DHCP server to run and enables clients to use network boot


# ddns
only give config file will won confluence a lot about the ddns . this is for my self memon 

```bash
{
    "DhcpDdns": {
        "ip-address": "127.0.0.1",
        "port": 53001,
        "dns-server-timeout": 100,
        "ncr-protocol": "UDP",
        "ncr-format": "JSON",
        "tsig-keys": [
            {
            	// is a name that you require use that next
                "name": "key_name",
                // algorithm I give the value is HMAC-MD5
                "algorithm": "HMAC-MD5",
                // secret form your dns
                "secret": "GRf05X2O543RfcI9stJYxLPpt6aJERqGHaBPManfMr4="
            }
        ],
        "forward-ddns": {
            "ddns-domains": [
                {
                    "name": "doman",
                    "key-name": "key_name",
                    "dns-servers": [
                        {
                            "hostname": "",
                            "ip-address": "dnsserver_ip0",
                            "port": 53
                        },
                        {
                            "hostname": "",
                            "ip-address": "dnsserver_ip1",
                            "port": 53
                        }
                    ]
                }
            ]
        }
    }
}
```