# -*- mode: ruby -*# vi: set ft=ruby :
require 'yaml'
vagrantConfig = YAML.load_file 'Vagrantfile.config.yml'
Vagrant.configure("2") do |config|
    config.vm.box = "bento/ubuntu-16.04"

    config.vm.define "python" do |python|
        python.vm.network "private_network", ip: vagrantConfig['ip1']
        python.vm.hostname = "python"
    end

    config.vm.synced_folder "tests/", "/home/vagrant/tests", owner:"vagrant", group: "vagrant"
    config.vm.synced_folder "pydl/", "/home/vagrant/pydl", owner:"vagrant", group: "vagrant"

    # VirtualBox specific settings
    config.vm.provider "virtualbox" do |vb|
        vb.gui = false
        vb.memory = "1024"
        vb.cpus = 1
    end

    config.vm.provision "shell", inline: "sudo apt-get update -y"
    config.vm.provision "shell", inline: "sudo apt-get upgrade -y"
    
    config.vm.provision "shell", inline: "curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -"
    config.vm.provision "shell", inline: "sudo add-apt-repository \"deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable\""
    config.vm.provision "shell", inline: "sudo apt-get update"
    config.vm.provision "shell", inline: "apt-cache policy docker-ce"
    config.vm.provision "shell", inline: "sudo apt-get install -y docker-ce"
    config.vm.provision "shell", inline: "sudo usermod -aG docker ${USER}"
end


