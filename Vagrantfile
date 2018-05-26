ENV['VAGRANT_DEFAULT_PROVIDER'] = "aws"

Vagrant.configure("2") do |config|
  # Use the dummy box provided by the vagrant-aws plugin
  config.vm.box = "aws"

  # Name our machine
  config.vm.hostname = "ansible-controller"

  # Force aws to use rsync by default for faster setup
  config.vm.allowed_synced_folder_types = [:rsync]

  # Enter aws provider info
  config.vm.provider "aws" do |aws, override|
    # Credentials we set up locally
    aws.aws_profile = "vagrant"

    # EC2 keypair
    aws.keypair_name = "vagrant_kp"

    # AWS AMI number
    aws.ami = "ami-8d948ced"
    aws.instance_type = "t2.micro"
    aws.security_groups = [ "vagrant" ]
    override.ssh.username = "ubuntu"
    override.ssh.private_key_path = '~/.ssh/vagrant_kp.pem'
  end
end

