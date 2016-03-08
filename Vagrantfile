# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 80, host: 8888
  config.vm.network "forwarded_port", guest: 443, host: 44443
  config.vm.network "forwarded_port", guest: 49001, host: 8001
  config.ssh.forward_agent = true
  config.vm.network "private_network", ip: "192.168.33.20"

  config.vm.provider "virtualbox" do |vb|
   # Customize the amount of memory on the VM:
    vb.memory = "8192"
  end

  config.vm.synced_folder "/Users/plaks/GitHub/", "/home/vagrant/GitHub"
  config.vm.synced_folder "/Users/plaks/.aws", "/home/vagrant/.aws"

  #config.vm.provision "file", source: "~/.aws", destination: "~/.aws"

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install wget -y
    sudo apt-get install python-pip -y
    wget -O- https://get.docker.com/ | sh
    sudo usermod -aG docker

    git config --global user.email "plaks@turbine.com"
    git config --global user.name "Phil Laks"

    sudo ntpdate -s time.nist.gov

    sudo service ntp stop
    sudo ntpdate -s time.nist.gov
    sudo service ntp start
    #curl https://get.docker.com | bash

    # Install pip
    # sudo wget https://raw.github.com/pypa/pip/master/contrib/get-pip.py
    # sudo python get-pip.py

    # Install python setuptools
    curl https://bootstrap.pypa.io/ez_setup.py -o - | sudo python

    # Install coverage module for unittests
    sudo pip install coverage

    # Install frontend tools
    sudo apt-get install nodejs-legacy -y
    sudo apt-get install npm -y
    sudo npm install
    sudo npm install -g grunt-cli
    sudo npm install --save-dev mocha

  SHELL
end
