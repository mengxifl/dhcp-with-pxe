# nginx
This Nginx server is configured to only serve iPXE files.

It requires that the files be accessed through the path http://<host>/ipxefile.

Therefore, iPXE will load files from http://<host>/bootfiles/ipxefile/index.ipxe.


tip Do not trust any file that requires root or administrator privileges to run. Please find it by yourself

If you want those file please let me know.

```

nerdctl run -d -p 0.0.0.0:80:80 -v /ipxfile/ -v ./config:/etc/nginx/conf.d me-nginx-proxy:v0.3  /bin/sh  -c 'nginx -g "daemon off;"'


```

then the ipxefiles those is a example. 
```
set boot-url http://${next-server}
chain ${boot-url}/bootfiles/ipxefile/${serial:uristring}.ipxe || chain ${boot-url}/bootfiles/ipxefile/defmenu.ipxe
```

You can write a lot of script , let ipxe load them

netboot:
https://github.com/netbootxyz/netboot.xyz


Those is my script if you want them let me know