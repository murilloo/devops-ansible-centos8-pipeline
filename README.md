# devops-ansible-centos8-pipeline
Example pipeline using Vagrant for provisioning a VM running CentOS 8 and Ansible to execute a list of administrative Ops tasks related

## Requirements
- Vagrant >= 2.2.5 (https://www.vagrantup.com/downloads.html)
- Libvirt >= 5.1.0 (https://libvirt.org/sources/)
- Python version = 3.7.5
- Ansible = 2.9.2

## Known Issues
- Ansible *nmcli* module has [this issue](https://github.com/ansible/ansible/pull/62609) open. Please fix it first before using it.

## Tasks (Pending)
- To add a new disk with *1GiB*, to create a volume group and a logical volume on top of it with *EXT4* file system and to mount it on */nginx*
- To configure Nginx as web server in the secondary interface with Document root */nginx*
- To activate SELinux and ensure Nginx listen sockets have proper security contexts enabled
- To create an archive (.xz) from /usr/share/doc/xz and to extract it to */nginx* 

## Tasks (Completed)
- To create a second network interface *System eth1* with its *DNS* set to *1.1.1.1* **(Vagrantfile + Ansible)**
```
[vagrant@localhost ~]$ nmcli c s System\ eth1 | grep 1.1.1.1
ipv4.dns:                               1.1.1.1
IP4.DNS[2]:                             1.1.1.1
```
- To assign an additional *IPv4* address to the current *System eth0* interface of provisioned VM **(Ansible)**
```
[vagrant@localhost ~]$ nmcli c s System\ eth0 | grep -i ip4
IP4.ADDRESS[1]:                         192.168.121.7/32
IP4.ADDRESS[2]:                         192.168.121.104/24
```

