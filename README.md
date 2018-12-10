# Vagrant Ansible Desktop

Vagrant Ansible Desktop is a vagrant managed desktop environment in virtualbox meant for development.  It runs python with pip and docker by default.  It is meant to provide a working ubuntu linux based development environment that is repeatable between work environments.  

# Vagrant Box

The vagrant box image is built with packer from [boxcutter/ubuntu](https://github.com/boxcutter/ubuntu)

```
git clone https://github.com/boxcutter/ubuntu.git
cd ubuntu
packer build -only=virtualbox-iso -var-file=ubuntu1804-desktop.json ubuntu.json
vagrant box add --name ubuntu/1804-desktop box/virtualbox/ubuntu1804-desktop-0.1.0.box
```

# Startup

Starting up the environment is easy.

```
vagrant up
```

# Ansible

Ansible is included in this repository for vagrant to utilize the `ansible_local` provisioner to manage the system configuration.  External roles are added as submodules.  All roles are added to the `type-vagrant.yml` playbook which is the default playbook vagrant will run (defined in the Vagrantfile)

## External Role Reference

[geerlingguy.pip](https://galaxy.ansible.com/geerlingguy/pip)
[geerlingguy.docker](https://galaxy.ansible.com/geerlingguy/docker)
