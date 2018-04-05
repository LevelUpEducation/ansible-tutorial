# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<-SCRIPT
sudo yum update -y
sudo yum install -y epel-release
sudo yum install -y ansible
SCRIPT


Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.network :private_network, ip: "10.0.15.10"
  config.vm.provision "shell", inline: $script
end
