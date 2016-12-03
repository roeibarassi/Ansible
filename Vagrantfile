Vagrant.configure("2") do |config|
  config.vm.define "web01", primary: true do |web01|
    web01.vm.box = "ubuntu/trusty64"
    web01.vm.hostname = 'web01'
    web01.vm.box_url = "ubuntu/trusty64"

    web01.vm.network :private_network, ip: "192.168.56.101"
    web01.vm.network :forwarded_port, guest: 22, host: 10122, id: "ssh"


    web01.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 256]
      v.customize ["modifyvm", :id, "--name", "web01"]
    end
    
    config.vm.provision "ansible" do |ansible|
      ansible.sudo = true
      ansible.verbose = "v"
      ansible.limit = "webservers[0]"
      ansible.playbook = "apacheInstall.yml"
    end
  end

  config.vm.define "web02", autostart: true do |web02|
    web02.vm.box = "ubuntu/trusty64"
    web02.vm.hostname = 'web02'
    web02.vm.box_url = "ubuntu/trusty64"

    web02.vm.network :private_network, ip: "192.168.56.102"
    web02.vm.network :forwarded_port, guest: 22, host: 10123, id: "ssh"


    web02.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 256]
      v.customize ["modifyvm", :id, "--name", "web02"]
    end

    config.vm.provision "ansible" do |ansible|
      ansible.sudo = true
      ansible.verbose = "v"
      ansible.limit = "webservers[1]"
      ansible.playbook = "apacheInstall.yml"
    end
  end

  config.vm.define "haproxyLB", autostart: true do |haproxyLB|
    haproxyLB.vm.box = "ubuntu/trusty64"
    haproxyLB.vm.hostname = 'haproxyLB'
    haproxyLB.vm.box_url = "ubuntu/trusty64"

    haproxyLB.vm.network :private_network, ip: "192.168.56.103"
    haproxyLB.vm.network :forwarded_port, guest: 22, host: 10124, id: "ssh"


    haproxyLB.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 256]
      v.customize ["modifyvm", :id, "--name", "haproxyLB"]
    end
    
    config.vm.provision "ansible" do |ansible|
      ansible.sudo = true
      ansible.verbose = "v"
      ansible.playbook = "haproxyLB.yml"
    end
  end

end
