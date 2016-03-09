# -*- mode: ruby -*-
# vi: set ft=ruby :


# --- Configuration

BOX_IMAGE     = ENV['BOX_IMAGE']     || "ubuntu/trusty64"
BOX_NAME      = ENV['BOX_NAME']      || "devbox"
BOX_ADMIN     = ENV['BOX_ADMIN']     || "vagrant"
BOX_IP        = ENV['BOX_IP_ZONE']   || "192.200.200.200"
BOX_MEMORY    = ENV['BOX_MEMORY']    || "4096"
BOX_CPUS      = ENV['BOX_CPUS']      || "2"


# --- Vagrant

Vagrant.configure("2") do |config|

  config.vm.box = BOX_IMAGE

  config.vm.network "private_network", ip: BOX_IP

  config.vm.boot_timeout = 100

  config.vm.synced_folder '.', '/vagrant', disabled: true

  config.vm.provider :virtualbox do |vb|
    vb.gui = false
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
    vb.customize ["modifyvm", :id, "--memory", BOX_MEMORY]
    vb.customize ["modifyvm", :id, "--cpus", BOX_CPUS]
  end

  config.vm.provision :shell, inline: "apt-get update && sudo apt-get upgrade -y"

  config.vm.provision :docker
  config.vm.provision :docker_compose

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "vagrant.yml"
    ansible.sudo = true
  end
end
