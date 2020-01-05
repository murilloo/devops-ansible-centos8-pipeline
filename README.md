# devops-ansible-rhel8-pipeline
Example pipeline using Vagrant for provisioning a VM running RHEL 8.1 and Ansible to execute a list of administrative Ops tasks related

## Requirements
- Vagrant >= 2.2.5 (https://www.vagrantup.com/downloads.html)
- Libvirt >= 5.1.0 (https://libvirt.org/sources/)

## Tasks
- To properly configure a secondary network interface in the server
- To configure Nginx as web server with Document root /nginx
- To activate SELinux and ensure Nginx listen sockets have proper security contexts enabled
- To create a Physical Volumes, Logical Volumes with a standard partition XFS mounted

** Under development **
