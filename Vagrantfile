# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 80, host: 8888
  config.vm.network "forwarded_port", guest: 443, host: 44443
  config.vm.network "forwarded_port", guest: 49001, host: 8001
  config.ssh.forward_agent = true


  config.vm.provider "virtualbox" do |vb|
   # Customize the amount of memory on the VM:
    vb.memory = "8192"
  end

  config.vm.synced_folder "/Users/plaks/GitHub/github.turbine.com/plaks/", "/home/vagrant/Git"


  config.vm.provision "file", source: "~/.aws", destination: "~/.aws"

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install wget -y
    wget -O- https://get.docker.com/ | sh
    sudo usermod -aG docker

    sudo ntpdate -s time.nist.gov

    sudo service ntp stop
    sudo ntpdate -s time.nist.gov
    sudo service ntp start
    #curl https://get.docker.com | bash

    # Install pip
    sudo wget https://raw.github.com/pypa/pip/master/contrib/get-pip.py
    sudo python get-pip.py

  SHELL
end
