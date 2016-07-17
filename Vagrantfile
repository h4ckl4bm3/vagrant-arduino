# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  config.vm.box = "ubuntu/trusty64"
  # config.vm.box_check_update = false
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "public_network"

  config.vm.synced_folder "./arduino", "/arduino"

  config.vm.provider "virtualbox" do |vb|
     vb.memory = "1024"

     vb.customize ["modifyvm", :id, "--usb", "on"]
     vb.customize ["modifyvm", :id, "--usbehci", "on"]
     vb.customize ["usbfilter", "add", "0", "--target", :id, "--name", "USB2.0-Serial"]
  end

  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  config.vm.provision "shell", inline: <<-SHELL
     sudo apt-get update
     sudo apt-get install -y python-pip linux-image-extra-$(uname -r) 
     sudo pip install platformio
     sudo modprobe ch341
     platformio -f init -d /arduino/ --board nanoatmega328
     sudo cp /vagrant/src/main.cpp /arduino/src/main.cpp

     echo "Completed setup, if you would like to build the demo project, simply run"
     echo "--------------------------------------------"
     echo "vagrant ssh"
     echo "sudo platformio run -d /arduino/ --target upload"
     echo "sudo cat /dev/ttyUSB0"
     echo "--------------------------------------------"
  SHELL
end
