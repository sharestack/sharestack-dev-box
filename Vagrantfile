# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "raring64"

  config.vm.box_url = "https://dl.dropboxusercontent.com/u/547671/thinkstack-raring64.box"

  config.vm.network :forwarded_port, guest: 8000, host: 8000 # Django
  config.vm.network :forwarded_port, guest: 9000, host: 9000 # Django 2

  config.vm.network :forwarded_port, guest: 5432, host: 15432 # Postgres
  config.vm.network :forwarded_port, guest: 9200, host: 19200 # Elastic search

  #config.vm.network :public_network
  config.vm.network :private_network, ip: "192.168.100.45"

  config.vm.synced_folder "~/projects/sharestack", "/home/vagrant/projects"

  config.vm.provider :virtualbox do |vb|
     vb.customize ["modifyvm", :id, "--memory", "2048"]
     vb.customize ["modifyvm", :id, "--cpus", "2"]
     vb.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "main.yml"
    ansible.inventory_path = "hosts-vagrant"
    ansible.verbose = "v"
    ansible.host_key_checking = false
    #ansible.extra_vars = { 
    #    tb_private_key: "/my/ssh/key" # Default ~/.ssh/id_rsa
    #}
  end
end
