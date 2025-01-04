# -*- mode: ruby -*-
# vi: set ft=ruby :

###############################################################
# This Vagrantfile provisions an SME IT environment 
#
# Prerequisite: Packaging the following VMs into Vagrant boxes
#    - Server0
#    - Ubuntu Server 24.04
#    - Ubuntu Desktop 24.04
#    - Windows 11 Enterprise
#    =>
#    - server0.box
#    - ubuntu_24.04_server.box
#    - ubuntu_24.04_desktop.box
#    - windows_11_enterprise.box
#    
#    $ ./package_vm.sh
###############################################################

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

Vagrant.configure("2") do |config|
  ########### WAN Machines ###########
  # Configure "Server0"
  # Server0 runs pfSense (i.e., FreeBSD), which sets up the Firewall, DHCP, DNS and VPN services
  # NOTE: This VM needs to be started before other VMs
  config.vm.define "server0" do |server0|
    server0.vm.box = "server0.box"
    server0.vm.guest = :freebsd
    server0.vm.network "public_network", bridge: "enp2s0f0", use_dhcp_assigned_default_route: true, auto_config: false
    server0.vm.network "private_network", ip: "192.168.58.5" 
    server0.vm.network "private_network", ip: "192.168.59.5" 
    server0.ssh.username = "admin"
    server0.ssh.password = "ransomware"
    server0.ssh.insert_key = false
    server0.vm.synced_folder ".", "/vagrant", disabled: true
    server0.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.memory = 4096
      vb.cpus = 2
    end
  end 

  # Configure "PC0a"
  config.vm.define "pc0a" do |pc0a|
    pc0a.vm.box = "windows_11_enterprise.box"
    pc0a.vm.guest = :windows
    pc0a.vm.network "public_network", bridge: "enp2s0f0", use_dhcp_assigned_default_route: true, auto_config: false
    pc0a.vm.communicator = "winrm"
    pc0a.winrm.username = "User"
    pc0a.winrm.password = "ransomware"
    pc0a.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.memory = 4096
      vb.cpus = 4
    end
  end 

  # Configure "PC0b"
  config.vm.define "pc0b" do |pc0b|
    pc0b.vm.box = "ubuntu_24.04_desktop.box"
    pc0b.vm.network "public_network", bridge: "enp2s0f0", use_dhcp_assigned_default_route: true, auto_config: false
    #pc0b.vm.provision "shell", run: "always", inline: "sudo netplan apply"
    #pc0b.vm.provision "shell", run: "always", inline: "ifconfig enp0s3 192.168.4.200 netmask 255.255.255.0 up"
    pc0b.ssh.username = "user"
    pc0b.ssh.password = "ransomware"
    pc0b.ssh.insert_key = true
    pc0b.vm.synced_folder ".", "/vagrant", disabled: true
    #pc0b.vm.provision "shell", path: "setup_pc0b.sh" 
    pc0b.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.memory = 4096
      vb.cpus = 2
    end
  end 


  ########### LAN1 Machines ########### 
  # Configure "PC1"
  config.vm.define "pc1" do |pc1|
    pc1.vm.box = "windows_11_enterprise.box"
    pc1.vm.guest = :windows
    pc1.vm.network "private_network", type: "dhcp", auto_config: false
    pc1.vm.communicator = "winrm"
    pc1.winrm.username = "User"
    pc1.winrm.password = "ransomware"
    pc1.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.memory = 4096
      vb.cpus = 4
    end
  end 
  
  # Configure "PC2"
  config.vm.define "pc2" do |pc2|
    pc2.vm.box = "ubuntu_24.04_desktop.box"
    pc2.vm.network "private_network", type: "dhcp", auto_config: false
    #pc2.vm.provision "shell", run: "always", inline: "sudo netplan apply"
    #pc2.vm.provision "shell", run: "always", inline: "ifconfig enp0s3 192.168.59.101 netmask 255.255.255.0 up"
    pc2.ssh.username = "user"
    pc2.ssh.password = "ransomware"
    pc2.ssh.insert_key = true
    pc2.vm.synced_folder ".", "/vagrant", disabled: true
    #pc2.vm.provision "shell", path: "setup_pc2.sh" 
    pc2.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.memory = 4096
      vb.cpus = 2
    end
  end 


  ########### LAN2 Machines ########### 
  # Configure "Server1"
  config.vm.define "server1" do |server1|
    server1.vm.box = "ubuntu_24.04_server.box"
    server1.vm.network "private_network", type: "dhcp", auto_config: false
    #server1.vm.provision "shell", run: "always", inline: "sudo netplan apply"
    #server1.vm.provision "shell", run: "always", inline: "ifconfig enp0s8 192.168.59.101 netmask 255.255.255.0 up"
    server1.ssh.username = "user"
    server1.ssh.password = "ransomware"
    server1.ssh.insert_key = true
    server1.vm.synced_folder ".", "/vagrant", disabled: true
    #server1.vm.provision "shell", path: "setup_server1.sh" 
    server1.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.memory = 4096
      vb.cpus = 2
    end
  end 
  
  # Configure "Server2"
  config.vm.define "server2" do |server2|
    server2.vm.box = "ubuntu_24.04_server.box"
    server2.vm.network "private_network", type: "dhcp", auto_config: false
    #server2.vm.provision "shell", run: "always", inline: "sudo netplan apply"
    #server2.vm.provision "shell", run: "always", inline: "ifconfig enp0s8 192.168.59.102 netmask 255.255.255.0 up"
    server2.ssh.username = "user"
    server2.ssh.password = "ransomware"
    server2.ssh.insert_key = true
    server2.vm.synced_folder ".", "/vagrant", disabled: true
    #server2.vm.provision "shell", path: "setup_server2.sh" 
    server2.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.memory = 4096
      vb.cpus = 2
    end
  end 

  # Configure "Server3"
  config.vm.define "server3" do |server3|
    server3.vm.box = "ubuntu_24.04_server.box"
    server3.vm.network "private_network", type: "dhcp", auto_config: false
    #server3.vm.provision "shell", run: "always", inline: "sudo netplan apply"
    #server3.vm.provision "shell", run: "always", inline: "ifconfig enp0s8 192.168.59.103 netmask 255.255.255.0 up"
    server3.ssh.username = "user"
    server3.ssh.password = "ransomware"
    server3.ssh.insert_key = true
    server3.vm.synced_folder ".", "/vagrant", disabled: true
    #server3.vm.provision "shell", path: "setup_server3.sh" 
    server3.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.memory = 4096
      vb.cpus = 2
    end
  end 
  
  # Configure "Server4"
  config.vm.define "server4" do |server4|
    server4.vm.box = "ubuntu_24.04_server.box"
    server4.vm.network "private_network", type: "dhcp", auto_config: false
    #server4.vm.provision "shell", run: "always", inline: "sudo netplan apply"
    #server4.vm.provision "shell", run: "always", inline: "ifconfig enp0s8 192.168.59.104 netmask 255.255.255.0 up"
    server4.ssh.username = "user"
    server4.ssh.password = "ransomware"
    server4.ssh.insert_key = true
    server4.vm.synced_folder ".", "/vagrant", disabled: true
    #server4.vm.provision "shell", path: "setup_server4.sh" 
    server4.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.memory = 4096
      vb.cpus = 2
    end
  end 

end
