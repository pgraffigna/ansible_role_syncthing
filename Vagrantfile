# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true
    
  config.vm.define "master" do |m|
    m.vm.box = "geerlingguy/ubuntu1804"
    m.vm.network "private_network", ip: "192.168.60.10"
    m.vm.network "forwarded_port", guest: 8384, host:8384
    m.vm.hostname = "master"

    m.vm.provision "shell", inline: <<-SHELL 
    sudo echo 192.168.60.11 node | sudo tee -a /etc/hosts
    SHELL

    m.vm.provider :virtualbox do |vb|
      vb.name = "template"
      vb.memory = 4096
      vb.cpus = 2
      vb.check_guest_additions = false 
    end 
  end  
    
  config.vm.define "node" do |n|
    n.vm.box = "geerlingguy/ubuntu1804"
    n.vm.network "private_network", ip: "192.168.60.11"
    n.vm.network "forwarded_port", guest: 8384, host:8385
    n.vm.hostname = "node"
    
    n.vm.provision "shell", inline: <<-SHELL
    sudo echo 192.168.60.10 master | sudo tee -a /etc/hosts
    SHELL
  end  
end
