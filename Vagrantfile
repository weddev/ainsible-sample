# -*- mode: ruby -*-
# vi: set ft=ruby :
#Ansible Tutorial
#http://yteraoka.github.io/ansible-tutorial/

#$ vagrant ssh-config node1 > ssh_config
#$ scp -F ssh_config .vagrant/machines/node2/virtualbox/private_key node1:.ssh/id_rsa

Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.define :node1 do |node|
    node.vm.network :forwarded_port, guest: 22, host: 2001, id: "ssh"
    node.vm.network :private_network, ip: "192.168.33.11"

    node.vm.provision "shell", inline: <<-SHELL
      sudo apt-get install -y python-software-properties
      sudo apt-add-repository ppa:ansible/ansible
      sudo apt-get update
      sudo apt-get install -y ansible
    SHELL
  end

  config.vm.define :node2 do |node|
    node.vm.network :forwarded_port, guest: 22, host: 2002, id: "ssh"
    node.vm.network :forwarded_port, guest: 80, host: 8000, id: "http"
    node.vm.network :private_network, ip: "192.168.33.12"
  end

end
