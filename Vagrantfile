# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX_IP = "192.168.33.77"
HOSTNAME = "ntdev-centos7"

# Vagrant base box to use
BOX_BASE = "centos/7"

# Vagrant setting
BOX_CPU = 2
BOX_MEMORY = 2048
VAGRANTFILE_API_VERSION = "2"
DISKSIZE = "80GB"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = false

  config.vm.synced_folder "./ntdev", "/home/src"

  # disksize vagrant-plugin
  config.disksize.size = DISKSIZE

  # VirtualBox.
  config.vm.boot_timeout = 120
  config.vm.define "virtualbox" do |virtualbox|
    virtualbox.vm.hostname = HOSTNAME
    virtualbox.vm.box = BOX_BASE
    virtualbox.vm.network :private_network, ip: BOX_IP

    config.vm.provider :virtualbox do |vb|
      vb.gui = true
      vb.name = HOSTNAME
      vb.memory = BOX_MEMORY 
      vb.cpus = BOX_CPU
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize ["modifyvm", :id, "--ioapic", "on"]

      # allow symlink
      vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
    end
  end

end
