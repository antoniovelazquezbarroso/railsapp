#  README

# Run $ ansible-galaxy install -r requirements.yml to install required roles
# The installation folder is /roles because of the configuration in ansible.cfg

# To provision with vagrant run vagrant up

## Building the VMs
  1. Download and install [VirtualBox](https://www.virtualbox.org/wiki/Downloads).
  2. Download and install [Vagrant](http://www.vagrantup.com/downloads.html).
  3. [Mac/Linux only] Install [Ansible](http://docs.ansible.com/intro_installation.html).
  4. Run `ansible-galaxy install -r requirements.yml` in the current directory to get the required Ansible roles.
  5. Run `vagrant up` to build the VMs and configure the infrastructure.
  