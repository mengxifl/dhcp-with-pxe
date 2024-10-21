This repository is only an example that shows you how to set up Kea DHCP and configure it with a PXE server.

It includes some components.

## kea-dhcp
  Kea-DHCP is a DHCP server that I use to assign IP addresses to clients
  
  https://github.com/mengxifl/dhcp-with-pxe/blob/main/kea-dhcp/kea-dhcp.md

## tftp server
  I use this server to host so that  clients  can load those require file.
  
  https://github.com/mengxifl/dhcp-with-pxe/blob/main/tftp/tftp.md

## nginx  a web server
  I use Nginx to host some files so that clients can retrieve the files they need from this server.
  
  https://github.com/mengxifl/dhcp-with-pxe/blob/main/nginx/nginx.md
## start steps

client set to netboot ->  get an ipaddress and next server  -> get Boot file (dhcp.client-classes) -> Boot file will load(XClient_iPXE) -> auto load iPXE Menu (from self host http://<localhost>/bootfiles/ipxefile/index.ipxe) -> load system base kernel or Windows boot

## I had configuerd a PXE.
   If you want to see that plese tell me
