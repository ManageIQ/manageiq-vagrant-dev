# manageiq-vagrant-dev
Vagrantfile and scripts so you can start a developer environment for ManageIQ Vagrant.

## Introduction ##
The script is currently designed in the following way:

- Your should clone the environment into an empty directory with all the scripts in it (i.e. ~/Vagrant/manageiq-vagrant-dev)
- The script makes some suppositions
  - Vagrant is installed
  - Ansible is installed in your host machine
  - Virtualbox is installed

## The process ##

The Vagrant file will create a VM using fedora24-cloud as a basis and proceed to configure it for development:
- Configure the VM with 4 GB and 2 CPU
- Open port 3000 for UI management
- Open port 4000 for API management
- Copy the contents of ~/workspace/manageiq to /manageiq inside the appliance
- Install python (needed by Ansible) so the Ansible playbook.yml can be run
- Configure the OS and install everything needed for development
- Configure the database, start and enable it and add the user needed
- Configure rbenv and install ruby 2.3.1
- Verify if reboot is necessary and then reboot the machine

## Limitations ##
It won't run bin/setup to download the gems and run the database migration, so you can test them.
It won't execute rake evm:start to start the service that you will find in localhost:3000
Synchronization is only done once because the strategy is rsync (you need to call vagrant rsync to resynchronize)

## Adapting the Vagrantfile ##
- You can add additional folders to be synchronized
- It is possible to use other synchronization strategies. Many of them allow bidirectional synchronization so you can see your changes in real time
- You can change the resources in the VM

