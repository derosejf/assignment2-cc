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
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/xenial64"
  
  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL

  # config.vm.provision "shell", path: "bootstrap.sh"

  # let's copy our openrc file
  #config.vm.provision "file", source: "./.openrc", destination: "~/.openrc"

  # let's copy our pem file to the vagrant created guest
  config.vm.provision "file", source: "../.ssh/key_team5.pem", destination: "~/.ssh/key_team5.pem"

  # similarly copy whatever files you want to
  
  # We now use the Ansible provisioner to install software. It is assumed you
  # have a playbook called playbook_master.yml
  #
  # in the following, install= true will install ansible in the
  # created or provisioned guest vm. Once ansible is installed, any
  # additional configuration we plan to do will be taken from the
  # supplied playbook. Moreover, we can also tell ansible which
  # Inventory file it should use. This inventory file will appear in the
  # /vagrant directory (which is the same directory on your host that has
  # the vagrantfile but is mounted as /vagrant in the guest machine)
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "site.yml"
    ansible.verbose = true
    ansible.install = true  # installs ansible (and hence python on VM)
    ansible.limit = "all"
    ansible.inventory_path = "hosts"  # inventory file
    #ansible.start_at_task = "Master File acting on Horizon VM"
  end
end
