# Description
This is a vagrant project for running the Movidius Neural Compute Stick in a
linux virtul environment. Suitable for Mac OSX.

# Use
## Install vagrant 2.0.0 (or higher)

## Install virtualbox
* install VirtualBox 5.1.x
** Don't get VirtualBox 5.2.x
** https://www.vagrantup.com/docs/virtualbox/

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