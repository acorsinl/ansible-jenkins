# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.hostname = "nestor"
  config.vm.provision :shell, :inline => "echo -e '#{File.read("#{Dir.home}/.ssh/id_rsa.pub")}' >> '/home/vagrant/.ssh/authorized_keys'"
  config.ssh.private_key_path = "~/.ssh/id_rsa"
  config.ssh.forward_agent = true
  #config.vm.network :private_network, ip: "192.168.33.33"
  #config.vm.synced_folder "/Users/acorsinl/Documents/Workspace/Code/bin", "/opt/bin"
  config.vm.provider "virtualbox" do |v|
    v.name = "nestor"
    v.memory = 1024
    v.cpus = 2
  end
  config.vm.provision "ansible" do |ansible|
    ansible.inventory_path = "provisioning/hosts"
    ansible.playbook = "provisioning/playbook.yml"
    ansible.sudo = true
  end
end
