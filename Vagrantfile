# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # linux version
  config.vm.box = "precise64"
  config.vm.box_url = 'http://files.vagrantup.com/precise64.box'

  # network
  config.vm.network :private_network, ip: "192.168.33.69"

  # mount point
  config.vm.synced_folder ".", "/var/www", owner: "www-data", group: "www-data", :mount_options => ['dmode=777,fmode=777']

  # vm resources
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
    vb.customize ["modifyvm", :id, "--cpus", "2"]
  end

  # provision script
  config.vm.provision "shell", path: "./provision.sh"
  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

end
