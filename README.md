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
- To configure an additional IPv4 address to the current eth0 interface<br>  
- To create a partition, assign it to physical volume, then create LVM with a standard partition XFS mounted on */nginx*
- To configure Nginx as web server in the secondary interface with Document root */nginx*
- To activate SELinux and ensure Nginx listen sockets have proper security contexts enabled
- To create an archive (.xz) from /usr/share/doc/xz and to extract it to */nginx* 


** Under development **

