# -*- mode: ruby -*-
# vi: set ft=ruby :

if !Vagrant.has_plugin?("vagrant-reload")
    puts "'vagrant-reload' plugin is required"
    puts "This can be installed by running:"
    puts
    puts "vagrant plugin install vagrant-reload"
    puts
    exit
end

Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  config.vm.box = "boxcutter/ubuntu1604-desktop"
  config.vm.box_url = "https://atlas.hashicorp.com/boxcutter/boxes/ubuntu1604-desktop"
  #config.vm.network "forwarded_port", guest: 80, host: 8080
  #config.vm.synced_folder ".", "/vagrant", disabled: true
  
  config.vm.provider "virtualbox" do |vb|
    vb.name = "ubuntu_dev"
    vb.gui = true
    vb.cpus = "2"
    vb.memory = "8192"	# 8GB
	
	vb.customize ["modifyvm", :id, "--description", "https://github.com/dimuran/developer_env"]
	vb.customize ["modifyvm", :id, "--vram", "64"]
	vb.customize ["setextradata", :id, "CustomVideoMode1", "1920x1080x32"]
	vb.customize ["modifyvm", :id, "--accelerate3d", "off"]
	vb.customize ["modifyvm", :id, "--accelerate2dvideo", "off"]
	#vb.customize ["modifyvm", :id, "--nic1", "nat"]
	#vb.customize ["modifyvm", :id, "--usb", "off"]
	vb.customize ["modifyvm", :id, "--audio", "none"]
	vb.customize ["modifyvm", :id, "--vrde", "off"]
	vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
	vb.customize ["modifyvm", :id, "--draganddrop", "bidirectional"]
	#vb.customize ["modifyvm", :id, "--natpf1", "delete ssh"]
	#vb.customize ["modifyvm", :id, "--natpf1", "ssh,tcp,127.0.0.1,2222,,22"]
	
	#v50 GB vmdk
	#http://unix.stackexchange.com/questions/176687/set-storage-size-on-creation-of-vm-virtualbox
	#http://blog.lenss.nl/2012/09/resize-a-vagrant-vmdk-drive/
	
  end

  # Run Ansible from the Vagrant VM
  config.vm.provision "ansible_local" do |ansible|
    ansible.install_mode = true
	ansible.install_mode = "pip"
    ansible.verbose = true
	ansible.galaxy_role_file = "requirements.yml"
    ansible.playbook = "playbook.yml"
  end
  config.vm.provision :reload  #https://github.com/aidanns/vagrant-reload
end
