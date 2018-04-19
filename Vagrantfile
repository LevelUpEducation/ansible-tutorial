require 'yaml'
hosts = YAML.load_file('hosts.yml')
Vagrant.configure("2") do |config|
  config.hostmanager.enabled = false

  hosts.each do |host|
    # Loop over our hosts.yml file
    config.vm.define host["name"] do |config|
      config.vm.box = host["box"]
      config.vm.hostname = host["name"]
      config.vm.network :private_network, ip: host["ip"]
      if host["forward_port"]
        config.vm.network "forwarded_port", guest: 80, host: host["forward_port"]
      end
      config.vm.provider "virtualbox" do |vb|
        vb.memory = "256"
      end

      # Sync ansible folder
      if host["name"] == 'ansible-control'
        config.vm.synced_folder "ansible/", "/home/ansible/ansible"
      end

      # Run our provisioners

      # Ubuntu boxes need to have python 2 installed
      if host["box"] == 'ubuntu/xenial64'
        config.vm.provision "shell",  preserve_order: true,
          inline: "sudo apt-get update && sudo apt install -y python-minimal"
      end

      # set up the /etc/hosts file for sshing between machines
      # you can rerun on command line via `vagrant hostmangager`
      config.vm.provision :hostmanager

      # run our playbook that sets up ansible user and ssh keys
      config.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbook.yml"
        ansible.groups = {
          "controller" => ["ansible-control"]
        }
      end
    end
  end
end
