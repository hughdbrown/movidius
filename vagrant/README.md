# Description
This is a vagrant project for running the Movidius Neural Compute Stick in a
linux virtul environment. Suitable for Mac OSX.

# Use
## Install vagrant 2.0.0 (or higher)

## Install virtualbox
* Install VirtualBox 5.1.x
** Don't get VirtualBox 5.2.x
** https://www.vagrantup.com/docs/virtualbox/

## Install virtualbox extension
* Make sure the version matches VirtualBox

## Run VBoxManage to get particulars of Movidius USB drive
```
% VBoxManage list usbhost
Host USB Devices:

...
UUID:               b21a1564-5034-4860-9dfa-67136ade7343
VendorId:           0x03e7 (03E7)
ProductId:          0x2150 (2150)
Revision:           0.1 (0001)
Port:               1
USB version/speed:  0/High
Manufacturer:       Movidius Ltd.
Product:            Movidius MA2X5X
SerialNumber:       03e72150
Address:            p=0x2150;v=0x03e7;s=0x00002b88d11fa220;l=0x14100000
Current State:      Available
```

## Modify vagrantfile to describe your Movidius device

http://code-chronicle.blogspot.com/2014/08/connect-usb-device-through-vagrant.html
https://sonnguyen.ws/connect-usb-from-virtual-machine-using-vagrant-and-virtualbox/
```
```

## Add vagrant image
```
% vagrant box add "ubuntu/xenial64"
==> box: Loading metadata for box 'ubuntu/xenial64'
    box: URL: https://atlas.hashicorp.com/ubuntu/xenial64
==> box: Adding box 'ubuntu/xenial64' (v20171011.0.0) for provider: virtualbox
The box you're attempting to add already exists. Remove it before
adding it again or add it with the `--force` flag.

Name: ubuntu/xenial64
Provider: virtualbox
Version: 20171011.0.0
```


## Start vagrant
```
vagrant up --provider=VirtualBox
vagrant ssh
```

## Find ubuntu xenial password
```
more ~/.vagrant.d/boxes/ubuntu-VAGRANTSLASH-xenial64/20171011.0.0/virtualbox/Vagrantfile
```
https://askubuntu.com/questions/832137/ubuntu-xenial64-box-password


## Provision with Movidius script
```
sudo apt-get install make
mkdir -p ~/workspace
cd ~/workspace
git clone https://github.com/movidius/ncsdk.git
cd ~/workspace/ncsdk
make install
```
https://github.com/movidius/ncsdk/blob/master/docs/release_notes.md
