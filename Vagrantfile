# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Base VM OS configuration.
  config.vm.box = "geerlingguy/ubuntu1404"
  config.vm.synced_folder '.', '/vagrant', disabled: true
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |v|
    v.memory = 512
    v.cpus = 1
  end

  # Define required VMs with name and static private IP addresses.
  boxes = [
    { :name => "vm47", :ip => "192.168.2.47" },  # FOR MONITORING AND DB REPLICATION 
    { :name => "vm57", :ip => "192.168.2.57" },  # app1 RAILS, web AND db SERVER (MASTER)
    { :name => "vm67", :ip => "192.168.2.67" },  # app2 RAILS SERVER
#    { :name => "vm70", :ip => "192.168.2.70" }, # FOR FUTURE NEEDS (¿¿ ??)
  ]

  # Provision each of the VMs.
  boxes.each do |opts|
    config.vm.define opts[:name] do |config|
      config.vm.hostname = opts[:name]
      config.vm.network :private_network, ip: opts[:ip]

      # Provision all the VMs using Ansible after last VM is up.
      if opts[:name] == "vm67"
#      if opts[:name] == "vm70"         # The last vhost 
        config.vm.provision "ansible" do |ansible|
          ansible.playbook = "playbooks/configure.yml"
          ansible.inventory_path = "inventories/vagrant/inventory"
          ansible.limit = "all"
          ansible.extra_vars = {
            ansible_ssh_user: 'vagrant',
            ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
          }
          end
      end
    end
  end

end
