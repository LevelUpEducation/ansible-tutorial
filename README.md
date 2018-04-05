## Vagrant & Ansible playbooks
---

### Intro
Install vagrant and discuss providers (virtualbox or vmware)
A. Vagrant
  1. Make one machine use  `vagrant up`, `vagrant halt`, `vagrant destroy`
  2. Use mutli-machine to create a control machine and one other
  3. (possible) Show how to refactor this longer vagrant file into a yaml file
  4. Discuss different providers. (May want to show a quick demo of aws provider in case students computers cannot handle the 5+ machines that will need to be running at once during the class)
  5. Install Ansible on the control machine (probably should use shell provisioner to demonstrate that vagrant capability) and show how ssh does not work be default between our VMs. Use this to segueway into the intro to ansible playbook section
B. Playbooks
  1. Create a playbook that creates an ansible user and sets up that user/ssh keys on all new vms.
  2. Use vagrants built in provider to test the playbook
  3. Create a hosts file with groups for each tier and use a vagrant synced folder to add it to the control machine

```
vagrant init centos/7
vagrant up
```

### Notes
Using vlan 10.0.15.0/24 for this course.
Warning! Do not choose an IP that overlaps with any other IP space on your system. This can cause the network to not be reachable.


### Helpful links

https://www.vagrantup.com/downloads.html
https://app.vagrantup.com/centos/boxes/7
https://app.vagrantup.com/ubuntu/boxes/xenial64
http://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html
https://codebeautify.org/yaml-validator
http://searchitoperations.techtarget.com/tip/Learn-YAML-through-a-personal-example
