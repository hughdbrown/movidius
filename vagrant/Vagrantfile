# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  # config.vm.box = "base"
  config.vm.box = "ubuntu/xenial64"

    config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--usb", "on"]
      vb.customize ["modifyvm", :id, "--usbxhci", "on"]
      vb.customize ["usbfilter", "add", "0",
        "--target", :id,
        "--name", "Movidius Neural Compute Stick",
        "--manufacturer", "Movidius Ltd.",
        "--product", "Movidius MA2X5X",
        "--vendorid", "0x03e7",
        "--productid", "0x2150"
      ]
    
      # Docs here suggest a second USB filter:
      # https://movidius.github.io/ncsdk/VirtualMachineConfig.html
      # You can get this info with:
      # % VBoxManage showvminfo $(cat .vagrant/machines/default/virtualbox/id)
      vb.customize ["usbfilter", "add", "1",
        "--target", :id,
        "--name", "5d8ae144-9961-49b0-8f44-18bc1bcdccfd",
        "--active", "yes",
        "--manufacturer", "Movidius",
        # "--product", "Movidius MA2X5X",
        "--vendorid", "0x2150",
        "--productid", "0xf63b"
      ]
    end

  config.vm.provider "virtualbox" do |vb|
     # Customize the amount of memory on the VM:
     vb.memory = "4096"
  end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
