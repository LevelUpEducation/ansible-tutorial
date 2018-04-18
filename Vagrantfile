require 'yaml'
hosts = YAML.load_file('hosts.yml')
Vagrant.configure("2") do |config|
  config.hostmanager.enabled = false
  config.ssh.insert_key=false

  hosts.each do |host|
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
    end
  end

  config.vm.provision :hostmanager

  #config.vm.provision "ansible" do |ansible|
    #ansible.playbook = "playbook.yml"
    #ansible.extra_vars = {
      #ansible_python_interpreter: "/usr/bin/python3",
    #}
    #ansible.verbose = true
  #end

end
