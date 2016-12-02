# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.require_version ">= 1.8.5"

Vagrant.configure(2) do |config|
  config.vm.box = "box-cutter/ubuntu1604"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.hostname = "www.magento2.dev"
  config.vm.network "forwarded_port", guest: 3306, host: 3306

  # Virtual box config
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "2048"
    vb.cpus = 2
  end

  # install python2.7
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y python-simplejson
  SHELL

  # NFS share
  #config.vm.synced_folder "../magento2", "/home/vagrant/repos/magento2", type: "nfs"

  # Provisioning
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/playbook.yml"
    ansible.inventory_path = "ansible/hosts"
    ansible.limit = 'all'
    ansible.verbose = "v"
  end
end
