# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
 
  config.vm.box = "williamyeh/ubuntu-trusty64-docker"

  # Add forwarded ports
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "forwarded_port", guest: 18080, host: 18080
  config.vm.network "forwarded_port", guest: 19000, host: 19000
  config.vm.network "forwarded_port", guest: 5432, host: 5432
  config.vm.network "forwarded_port", guest: 18081, host: 18081
  config.vm.network "forwarded_port", guest: 8000, host: 8000
  config.vm.network "forwarded_port", guest: 12222, host: 12222
  config.vm.network "forwarded_port", guest: 4444, host: 4444

  config.vm.synced_folder ".", "/vagrant", disabled: false
  
  config.vm.provider "virtualbox" do |v|
    v.memory = 6144
    v.cpus = 2
  end

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