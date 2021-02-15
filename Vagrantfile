# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.require_version ">= 1.7.0"

Vagrant.configure("2") do |config|

  # config.vm.box = "ubuntu/trusty64"
  config.vm.box = "bento/ubuntu-18.04" 

  config.ssh.insert_key = false  
  # config.vm.box_check_update = false
  config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  # config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "public_network"
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "7168"
    vb.cpus = 1
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.become = true
    ansible.verbose = "v"
    ansible.playbook = "playbook.yml"
    ansible.extra_vars = { 
      ansible_ssh_user: 'vagrant',
      ansible_python_interpreter: "/usr/bin/python3"
    }
    ansible.sudo = true
    # ansible.inventory_path = "role-httpd/tests/inventory"
  end

end
