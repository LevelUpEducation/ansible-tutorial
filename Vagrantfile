Vagrant.configure("2") do |config|
  # Use the dummy box provided by the vagrant-aws plugin
  config.vm.box = "aws"
  # Force aws to use rsync by default for faster setup
  config.vm.allowed_synced_folder_types = [:rsync]

  config.vm.define "controller" do |controller|
    controller.vm.box = 'aws'
    controller.vm.hostname = 'controller'

    controller.vm.provider 'aws' do |aws, override|
      aws.aws_profile = "vagrant"
        # Specify SSH keypair to use
      aws.keypair_name = 'vagrant_kp'


      # Specify region, AMI ID, Instance and security group
      aws.ami = 'ami-34332854'
      aws.instance_type = 't2.micro'
      aws.security_groups = [ 'vagrant' ]
      aws.ssh_host_attribute = "public_ip_address"

      # Specify username and private key path
      override.ssh.username = 'ansible'
      override.ssh.private_key_path = 'ssh/vagrant_kp.pem'
    end
  end

  config.vm.define "pg" do |pg|
    pg.vm.box = 'aws'
    pg.vm.hostname = 'pg'

    pg.vm.provider 'aws' do |aws, override|
      aws.aws_profile = "vagrant"
        # Specify SSH keypair to use
      aws.keypair_name = 'vagrant_kp'

      # Specify region, AMI ID, Instance and security group
      aws.ami = 'ami-df2932bf'
      aws.instance_type = 't2.micro'
      aws.security_groups = [ 'vagrant' ]
      aws.ssh_host_attribute = "public_ip_address"

      # Specify username and private key path
      override.ssh.username = 'ansible'
      override.ssh.private_key_path = 'ssh/vagrant_kp.pem'
    end
  end

  config.vm.provision :hostmanager

end
