# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.define "ansible" do |ansible|
      ansible.vm.box = "geerlingguy/centos7"
      ansible.vm.network "private_network", type: "static", ip: "192.168.99.10"
      ansible.vm.hostname = "ansible"
      ansible.vm.provider "virtualbox" do |v|
        v.name = "ansible"
        v.memory = 2048
        v.cpus = 2
      end
      ansible.vm.provision :shell do |shell|
        shell.path = "install_ansible.sh"
        shell.args = ["master", "192.168.99.10"]
      end
    end
    clients=2
    ram_client=2048
    cpu_client=2
    (1..clients).each do |i|
      config.vm.define "client#{i}" do |client|
        client.vm.box = "geerlingguy/centos7"
        client.vm.network "private_network", type: "static", ip: "192.168.99.1#{i}"
        client.vm.hostname = "client#{i}"
        client.vm.provider "virtualbox" do |v|
          v.name = "client#{i}"
          v.memory = ram_client
          v.cpus = cpu_client
        end
        client.vm.provision :shell do |shell|
          shell.path = "install_ansible.sh"
          shell.args = ["node", "192.168.99.10"]
        end
      end
    end
  end