hosts = ['centos']

Vagrant.configure('2') do |config|

  config.vm.box = 'generic/rhel8'
  config.vm.define hostname = 'rhel8'
  config.vm.provider :libvirt do |libvirt|
    libvirt.driver = 'kvm'
    libvirt.cpus = 2
    libvirt.memory = '1024'
  end
end
