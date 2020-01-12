hosts = ['centos']

Vagrant.configure('2') do |config|

  config.vm.box = 'centos/8'
  config.vm.define hostname = 'centos8'
  config.vm.provider :libvirt do |libvirt|
    libvirt.driver = 'kvm'
    libvirt.cpus = 2
    libvirt.memory = '1024'
    libvirt.storage :file, :size => '1G'
  end

  config.vm.define :centos8 do |centos8|
    centos8.vm.network :private_network,
      :type => "dhcp",
      :libvirt__network_address => '10.20.30.0'
  end

  config.vm.provision 'ansible' do |ansible|
        ansible.limit = hostname
        ansible.compatibility_mode = '2.0'
        ansible.verbose = false
        ansible.playbook = 'main.yml'
   end

end
