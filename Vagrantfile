# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
sudo apt-get update

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10

sudo apt-get -y install software-properties-common python-software-properties python g++ make

sudo apt-get -y install language-pack-de

sudo add-apt-repository -y ppa:git-core/ppa

# Add node.js sources
curl -sL https://deb.nodesource.com/setup_4.x | bash -

# vim
sudo apt-get update

# update git
sudo apt-get -y install git

sudo apt-get install -y nodejs

SCRIPT

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu/trusty64"

  # forward MongoDB
  config.vm.network "forwarded_port", guest: 27017, host: 27018

  config.vm.network "private_network", ip: "192.168.50.100"

  config.vm.hostname = "nodejs.vm"

  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'" # avoids 'stdin: is not a tty' error.

  config.vm.provision "shell", inline: $script

  # If true, then any SSH connections made will enable agent forwarding.
  config.ssh.forward_agent = true

  config.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 2
   end
end
