# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "ubuntu/xenial64"

    config.ssh.insert_key = false
    config.ssh.private_key_path = ["~/.ssh/id_rsa", "~/.vagrant.d/insecure_private_key"]
    config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
    config.vm.provision "file", source: "~/.ssh/id_rsa", destination: "~/.ssh/id_rsa"
    config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
    config.vm.provision "shell", inline: <<-EOC
      sudo sed -i -e "\\#PasswordAuthentication yes# s#PasswordAuthentication yes#PasswordAuthentication no#g" /etc/ssh/sshd_config
      sudo service ssh restart
    EOC

    config.vm.define "jenkins" do |machine|
        machine.vm.box = "jenkins_with_plugins"
        machine.vm.host_name = "jenkins"
        machine.vm.network :private_network, ip: "192.168.33.11"
 #       machine.vm.provision "shell", inline: "sudo usermod -aG docker jenkins"
 #       machine.vm.provision "shell", inline: "sudo service jenkins restart"
    end

    config.vm.define "mgr1" do |machine|
        machine.vm.box = "docker_manager"
        machine.vm.host_name = "mgr1"
        machine.vm.network :private_network, ip: "192.168.33.12"
    end

    config.vm.define "node1" do |machine|
        machine.vm.box = "docker_node"
        machine.vm.host_name = "node1"
        machine.vm.provider "virtualbox" do |v|
          v.memory = 512
          v.cpus = 1
        end
        machine.vm.network :private_network, ip: "192.168.33.13"
    end

    config.vm.define "node2" do |machine|
        machine.vm.box = "docker_node"
        machine.vm.host_name = "node2"
        machine.vm.provider "virtualbox" do |v|
          v.memory = 512
          v.cpus = 1
        end
        machine.vm.network :private_network, ip: "192.168.33.14"
    end

    config.vm.define "mongodb1" do |machine|
        machine.vm.box = "mongodb"
        machine.vm.host_name = "mongodb1"
        machine.vm.network :private_network, ip: "192.168.33.10"
    end

end