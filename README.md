# devops-ansible-centos8-pipeline
Example pipeline using Vagrant for provisioning a VM running CentOS 8 and Ansible to execute a list of administrative Ops tasks related

## Requirements
- Vagrant >= 2.2.5 (https://www.vagrantup.com/downloads.html)
- Libvirt >= 5.1.0 (https://libvirt.org/sources/)
- Python version = 3.7.5
- Ansible = 2.9.2

## Known Issues
- Ansible *nmcli* module has [this issue](https://github.com/ansible/ansible/pull/62609) open. Please fix it first before using it.

## Tasks

#### 1) To create a second network interface *System eth1* with its *DNS* set to *1.1.1.1* 
```
[vagrant@localhost ~]$ nmcli c s System\ eth1 | grep 1.1.1.1
ipv4.dns:                               1.1.1.1
IP4.DNS[2]:                             1.1.1.1
```
#### 2) To assign an additional *IPv4* address to the current *System eth0* interface of provisioned VM
```
[vagrant@localhost ~]$ nmcli c s System\ eth0 | grep -i ip4
IP4.ADDRESS[1]:                         192.168.121.7/32
IP4.ADDRESS[2]:                         192.168.121.104/24
```
#### 3) To add a new disk with *1GiB*, to create a volume group with *5000Mib* size, then logical volume with *250Mib* with *EXT4* file system and to mount it on */nginx*
```
[vagrant@localhost ~]$ sudo pvs
  PV         VG           Fmt  Attr PSize   PFree  
  /dev/vdb1  vagrant_demo lvm2 a--  496.00m 244.00m
  
[vagrant@localhost ~]$ sudo lvs
  LV   VG           Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  vol1 vagrant_demo -wi-ao---- 252.00m                                                    

[vagrant@localhost ~]$ mount | grep nginx
/dev/mapper/vagrant_demo-vol1 on /nginx type ext4 (rw,relatime,seclabel)
```

#### 4) To configure Nginx as web server in the secondary interface with Document root */nginx*. Make sure SELinux is *active* and security contexts are properly configured.
```
[vagrant@localhost ~]$ getenforce
Enforcing

[vagrant@localhost /]$ ls -laZ | grep nginx
drwxr-xr-x.   3 nginx   nginx   system_u:object_r:httpd_sys_rw_content_t:s0       1024 Jan 12 14:05 nginx
[vagrant@localhost /]$ 

[vagrant@localhost ~]$ curl -v http://192.168.121.7:8080/
*   Trying 192.168.121.7...
* TCP_NODELAY set
* Connected to 192.168.121.7 (192.168.121.7) port 8080 (#0)
> GET / HTTP/1.1
> Host: 192.168.121.7:8080
> User-Agent: curl/7.61.1
> Accept: */*
> 
< HTTP/1.1 200 OK
< Server: nginx/1.14.1
< Date: Sun, 12 Jan 2020 14:06:45 GMT
< Content-Type: text/html
< Transfer-Encoding: chunked
< Connection: keep-alive
< 
<html>
<head><title>Index of /</title></head>
...
</html>
* Connection #0 to host 192.168.121.7 left intact
```

#### 5) To create an archive (.xz) from /usr/share/doc/xz and to extract it to */nginx* 
```
[vagrant@localhost nginx]$ pwd
/nginx

[vagrant@localhost nginx]$ ls -1
xz

[vagrant@localhost nginx]$ ls -lrt *
total 143
-rw-r--r--. 1 root root 43305 Apr 29  2018 xz-file-format.txt
-rw-r--r--. 1 root root  4040 Apr 29  2018 TODO
-rw-r--r--. 1 root root  2487 Apr 29  2018 THANKS
-rw-r--r--. 1 root root 13526 Apr 29  2018 README
-rw-r--r--. 1 root root  5689 Apr 29  2018 lzma-file-format.txt
-rw-r--r--. 1 root root  7427 Apr 29  2018 history.txt
-rw-r--r--. 1 root root  9411 Apr 29  2018 faq.txt
-rw-r--r--. 1 root root 18092 Apr 29  2018 COPYING.GPLv2
-rw-r--r--. 1 root root  2775 Apr 29  2018 COPYING
-rw-r--r--. 1 root root  1043 Apr 29  2018 AUTHORS
-rw-r--r--. 1 root root 21413 Apr 29  2018 NEWS
```
