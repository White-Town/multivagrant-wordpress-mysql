# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # Global VM provider configuration for VirtualBox
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"  # Allocate 2048 MB of RAM to each VM
    vb.cpus = 2         # Assign 2 CPUs to each VM
  end

  # Global box configuration for VMs (using Ubuntu 20.04)
  config.vm.box = "ubuntu/focal64"

  # Global provisioning script to be run on all VMs (common setup)
  config.vm.provision "shell", path: "scripts/common.sh"

  # Web Server VM (Apache2 with WordPress)
  config.vm.define "web" do |web_config|
    # Set the hostname of the web server VM
    web_config.vm.hostname = "apache"
    
    # Set a private network IP for the web server VM
    web_config.vm.network "private_network", ip: "192.168.56.6"
    
    # Sync the local web files directory to the web server VM
    web_config.vm.synced_folder "./web_files", "/home/vagrant/web_vm_files"
    
    # Provision the web server with a specific script (e.g., install Apache2, PHP, WordPress)
    web_config.vm.provision "shell", path: "scripts/web.sh"  # Web server specific script
  end

  # Database Server VM (MySQL)
  config.vm.define "db" do |db_config|
    # Set the hostname of the database server VM
    db_config.vm.hostname = "db"
    
    # Set a private network IP for the database server VM
    db_config.vm.network "private_network", ip: "192.168.56.7"
    
    # Sync the local database files directory to the database server VM
    db_config.vm.synced_folder "./db_files", "/home/vagrant/db_vm_files"
    
    # Provision the database server with a specific script (e.g., install MySQL)
    db_config.vm.provision "shell", path: "scripts/db.sh"  # Database specific script
  end

  # Uncomment the following line to configure a public network if needed
  # config.vm.network "public_network"
end