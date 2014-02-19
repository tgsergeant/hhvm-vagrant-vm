# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

guest_ip = "33.33.33.10"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.network :forwarded_port, guest: 80, host: 9080
  config.vm.network :forwarded_port, guest: 81, host: 9081

  config.vm.network :private_network, ip: "192.168.33.10"
  config.vm.synced_folder "codebases/hhvm/", "/home/vagrant/dev/hhvm", type: "nfs"

  config.vm.provider :virtualbox do |vb|
    vb.name = "HipHop VM"
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--cpus", "4"]
    vb.customize ["modifyvm", :id, "--hwvirtex", "on"]
    vb.customize ["modifyvm", :id, "--nestedpaging", "on"]
  end

  config.vm.provision :shell, path: "postinstall.sh"

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.auto_detect = true
    config.cache.enable_nfs  = true
  end
end
