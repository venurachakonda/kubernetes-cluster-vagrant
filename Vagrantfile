# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "venurachakonda/ubuntu16"
  config.ssh.insert_key = false

  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 2
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--cableconnected1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  # Define Kubernetes VMs with static IP addresses
  servers = [
    { :name => "kube-master", :ip => "192.168.66.20" },
    { :name => "kube-worker1", :ip => "192.168.66.41" },
    { :name => "kube-worker2", :ip => "192.168.66.42" }
  ]

  # spin up each of VMs
  servers.each do |opts|
    config.vm.define opts[:name] do |config|
      config.vm.host_name = opts[:name]
      config.vm.network "private_network", ip: opts[:ip]

      # After last VM is up, proceed with provision of all VMs with ansible

      if opts[:name] == "kube-worker2"
        config.vm.provision :ansible do |ansible|
          ansible.playbook = "playbooks/playbook.yml"
          ansible.inventory_path = "playbooks/inventory"
          ansible.become = true
          ansible.limit = "all"
          ansible.compatibility_mode = "2.0"
        end
      end
    end
  end
end
