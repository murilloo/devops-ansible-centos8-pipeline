# devops-ansible-centos8-pipeline
Example pipeline using Vagrant for provisioning a VM running CentOS 8 and Ansible to execute a list of administrative Ops tasks related

## Requirements
- Vagrant >= 2.2.5 (https://www.vagrantup.com/downloads.html)
- Libvirt >= 5.1.0 (https://libvirt.org/sources/)

## Tasks
- To properly configure a *secondary* network interface in the server<br>
    __Please check [this issue](https://github.com/ansible/ansible/pull/62609) from Ansible nmcli module__
- To create a partition, assign it to physical volume, then create LVM with a standard partition XFS mounted on */nginx*
- To configure Nginx as web server in the secondary interface with Document root */nginx*
- To activate SELinux and ensure Nginx listen sockets have proper security contexts enabled
- To create an archive (.xz) from /usr/share/doc/xz and to extract it to */nginx* 


** Under development **

