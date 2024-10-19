# tftp

I use this server to host so that  clients  can load those require file.

Use Docker to run these servers for testing purposes only. They should run in the foreground
```
nerdctl run -it --rm -d -p 0.0.0.0:69:69/udp -v /boot_files/:/tftpfile  alpine  /bin/sh
sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
apk update && apk upgrade
apk add --no-cache tftp-hpa bash
in.tftpd --ipv4 --address 0.0.0.0:69  -L -vv -s --secure -s  /tftpfile
```

I will not give your BOOT FILE. Tip Do not trust any file that requires root or administrator privileges to run. Please find it by yourself

