# run if you get any provider errors
# `export ENV['VAGRANT_DEFAULT_PROVIDER'] = "aws"`
# AMI ids
#levelup-ansible-ubuntu: ami-34332854
#levelup-ansible-centos:ami-df2932bf

require "yaml"
hosts = YAML.load_file("hosts.yml")

Vagrant.configure("2") do |config|
  config.hostmanager.enabled = false
  # Use the dummy box provided by the vagrant-aws plugin
  config.vm.box = "aws"
  # Force aws to use rsync by default for faster setup
  config.vm.allowed_synced_folder_types = [:rsync]

  hosts.each do |host|
   config.vm.define host["name"] do |conf|
     conf.vm.hostname = host["name"]

      conf.vm.provider "aws" do |aws, override|
        # Specify Profile SSH keypair to use
        aws.aws_profile = "vagrant"
        aws.keypair_name = "vagrant_kp"

        # Specify region, AMI ID, Instance and security group
        aws.ami = host["ami"]
        aws.instance_type = "t2.micro"
        aws.security_groups = ["vagrant"]

        # Needed for hostmanager to work
        aws.ssh_host_attribute = "public_ip_address"

        # Specify username and private key path
        override.ssh.username = "ansible"
        override.ssh.private_key_path = "ssh/vagrant_kp.pem"
      end


   end
 end

  config.vm.provision :hostmanager

end
