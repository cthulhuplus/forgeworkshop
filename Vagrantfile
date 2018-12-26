# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.define "reverseproxy" do |reverseproxy|
#    reverseproxy.vm.box = "geerlingguy/centos7"
    reverseproxy.vm.box = "centos/7"
    reverseproxy.vm.network "forwarded_port", guest: 80, host: 8880
    reverseproxy.vm.network "private_network", ip: "172.31.255.2"
    reverseproxy.vm.provider :virtualbox do |v|
      v.memory = 512
      v.cpus = 1
    end
  reverseproxy.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "reverseproxy.yml"
    ansible.galaxy_role_file = "rprequirements.yml"
    ansible.galaxy_roles_path = "/etc/ansible/roles"
    ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"
  end
  end

  config.vm.define "apache" do |apache|
#    reverseproxy.vm.box = "geerlingguy/centos7"
    apache.vm.box = "centos/7"
#    reverseproxy.vm.network "forwarded_port", guest: 80, host: 8880
    apache.vm.network "private_network", ip: "172.31.255.3"
    apache.vm.provider :virtualbox do |v|
      v.memory = 512
      v.cpus = 1
    end
  apache.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "apache.yml"
    ansible.galaxy_role_file = "apacherequirements.yml"
    ansible.galaxy_roles_path = "/etc/ansible/roles"
    ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"
  end
  end

  config.vm.define "mysql" do |mysql|
#    reverseproxy.vm.box = "geerlingguy/centos7"
    mysql.vm.box = "centos/7"
#    reverseproxy.vm.network "forwarded_port", guest: 80, host: 8880
    mysql.vm.network "private_network", ip: "172.31.255.4"
    mysql.vm.provider :virtualbox do |v|
      v.memory = 512
      v.cpus = 1
    end
  mysql.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "mysql.yml"
    ansible.galaxy_role_file = "mysqlrequirements.yml"
    ansible.galaxy_roles_path = "/etc/ansible/roles"
    ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"
  end
  end

  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
#  config.vm.box = "centos/7"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

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

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
