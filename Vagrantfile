# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 80, host: 8888
  config.vm.network "forwarded_port", guest: 443, host: 44443
  config.vm.network "forwarded_port", guest: 49001, host: 8001
  config.ssh.forward_agent = true
  config.vm.network "private_network", ip: "192.168.19.86"

  config.vm.provider "virtualbox" do |vb|
   # Customize the amount of memory on the VM:
    vb.memory = "8192"
  end

  config.vm.synced_folder "/Users/phil/dev/", "/home/vagrant/dev"
  config.vm.synced_folder "/Users/phil/.aws", "/home/vagrant/.aws"

  #config.vm.provision "file", source: "~/.aws", destination: "~/.aws"

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get upgrade -y
    sudo apt-get update
    echo '----------------INSTALLING WGET--------------'
    sudo apt-get install wget -y
    echo '----------------INSTALLING PYTHON--------------'
    sudo apt-get install python -y
    echo '----------------INSTALLING PIP--------------'
    #sudo apt-get install python-pip -y
    wget https://bootstrap.pypa.io/get-pip.py
    python get-pip.py
    echo '----------------INSTALLING CURL--------------'
    sudo apt-get install curl
    echo '----------------INSTALLING DOCKER--------------'
    curl -fsSL https://get.docker.com/ | sh
    #wget -O- https://get.docker.com/ | bash
    sudo usermod -aG docker vagrant
    echo '----------------TESTING DOCKER--------------'
    docker run hello-world
    echo '----------------INSTALLING DOCKER-COMPOSE--------------'
    sudo pip install docker-compose

    echo '----------------INSTALLING GIT--------------'
    sudo apt-get install git
    git config --global user.email "plaks@turbine.com"
    git config --global user.name "Phil Laks"

    echo '----------------FIXING TIME--------------'
    sudo service ntp stop
    sudo ntpdate -s time.nist.gov
    sudo service ntp start
    #curl https://get.docker.com | bash

    # Install pip
    # sudo wget https://raw.github.com/pypa/pip/master/contrib/get-pip.py
    # sudo python get-pip.py

    # Install python setuptools
    echo '----------------INSTALLING PYTHON SETUP TOOLS--------------'
    curl https://bootstrap.pypa.io/ez_setup.py -o - | sudo python

    # Install coverage module for unittests and pytest for pytests, flask testing for... you get the idea
    echo '----------------INSTALLING PYTHON COVERAGE--------------'
    sudo pip install coverage
    echo '----------------INSTALLING PYTHON PYTEST & TIMEOUT EXTENSION--------------'
    sudo pip install pytest
    # sudo pip install pytest-timeout
    echo '----------------INSTALLING PYTHON FLASK--------------'
    sudo pip install Flask
    echo '----------------INSTALLING PYTHON FLASK-TESTING--------------'
    sudo pip install Flask-Testing
    echo '----------------INSTALLING BOTO3--------------'
    sudo pip install boto3

    # Install frontend tools
    echo '----------------INSTALLING NODEJS-LEGACY--------------'
    sudo apt-get install nodejs-legacy -y
    #sudo apt-get install npm -y
    echo '----------------CLEANING UP APT--------------'
    sudo apt-get autoremove -y
    echo '----------------INSTALLING NPM--------------'
    curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
    sudo apt-get install -y nodejs
    #sudo npm install npm
    #sudo npm install -g grunt-cli
    #sudo npm install --save-dev mocha
    echo '--------------VAGRANTFILE PROVISION COMPLETE, LOGGING OUT--------------'
    logout
  SHELL
end
