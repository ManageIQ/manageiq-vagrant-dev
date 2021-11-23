ENV['VAGRANT_DEFAULT_PROVIDER'] = 'virtualbox'
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = "fedora/33-cloud-base"
  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  #config.vm.network "forwarded_port", guest: 80, host:   13080
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "forwarded_port", guest: 4000, host: 4000
  #config.vm.network "forwarded_port", guest: 443, host: 13443

  config.vm.provider "virtualbox" do |vb|
     vb.memory = 6144
     vb.cpus = 2
     vb.name = "manageiq-dev"
  end
  
  config.vm.provider "libvirt" do |vm|
     vm.memory = 6144
     vm.cpus = 2
  end

  config.vm.hostname = "miqdev"

  # There are bidirectional synchronization types that should be preferred if available
  config.vm.synced_folder "~/workspace/manageiq/", "/home/vagrant/manageiq", type: "rsync"

  # Install prerequisites for Ansible
   config.vm.provision "shell", path: "scripts/initiation.sh"

  # Run Ansible from the Vagrant VM 
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "scripts/playbook.yml"
  end

  config.vm.provision "shell", privileged: false, inline: <<-EOF
    echo "Vagrant Box provisioned!"
    echo "Please do $ vagrant ssh, your code will be in ~/manageiq"
    echo "and do $ bin/setup to finish configuration"
    echo "Server can be started with $ bundle exec rake evm:start"
    echo "Local server address is http://localhost:3000"
    echo "There is additional information in http://manageiq.org/docs/guides/developer_setup"
  EOF
end
