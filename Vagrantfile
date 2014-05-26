# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # HTTP
  config.vm.network "forwarded_port", guest: 80, host: 80
  # MySQL
  config.vm.network "forwarded_port", guest: 3306, host: 3306
  # Mongo
  config.vm.network "forwarded_port", guest: 27017, host: 27017
	
  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.42.42"

  # Install HHVM
  config.vm.provision "shell", inline: <<-shell
    apt-get update
    apt-get install python-software-properties  -y --force-yes
    add-apt-repository ppa:mapnik/boost
    wget -O - http://dl.hhvm.com/conf/hhvm.gpg.key | sudo apt-key add -
    echo deb http://dl.hhvm.com/ubuntu precise main | sudo tee /etc/apt/sources.list.d/hhvm.list
    apt-get update
    apt-get install hhvm-nightly -y --force-yes
    apt-get install screen vim -y --force-yes
    debconf-set-selections <<< 'mysql-server-5.5 mysql-server/root_password password pa$$'
    debconf-set-selections <<< 'mysql-server-5.5 mysql-server/root_password_again password pa$$'
    apt-get install mysql-server -y --force-yes
  shell
end
