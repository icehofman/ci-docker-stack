# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
 
  config.vm.box = "williamyeh/ubuntu-trusty64-docker"

  # Add forwarded ports
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "forwarded_port", guest: 8888, host: 8888
  config.vm.network "forwarded_port", guest: 9000, host: 9000
  config.vm.network "forwarded_port", guest: 5432, host: 5432
  config.vm.network "forwarded_port", guest: 8181, host: 8181
  config.vm.network "forwarded_port", guest: 4444, host: 4444

  config.vm.synced_folder ".", "/vagrant", disabled: false
  
  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
    v.cpus = 2
  end

  config.vm.provision "shell", inline: "swapoff -a"
  config.vm.provision "shell", inline: "fallocate -l 2G /swapfile"
  config.vm.provision "shell", inline: "chmod 600 /swapfile"
  config.vm.provision "shell", inline: "mkswap /swapfile"
  config.vm.provision "shell", inline: "swapon /swapfile"

  config.vm.provision :docker

  # Install the plugin: vagrant plugin install vagrant-docker-compose
  config.vm.provision :docker_compose,
    yml: [
      "/vagrant/docker-compose-ci.yml",
      "/vagrant/docker-compose-selenium.yml"
    ],
    rebuild: true,
    run: "always"
   
end