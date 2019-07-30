# Vagrant Ansible Desktop

Vagrant Ansible Desktop is a vagrant managed desktop environment in virtualbox meant for development.  It runs python with pip and docker by default.  It is meant to provide a working ubuntu linux based development environment that is repeatable between work environments.  

# Vagrant Box

The vagrant box image is built with packer from [boxcutter/ubuntu](https://github.com/boxcutter/ubuntu)

In this repo you will find `boxcutter/ubuntu1904-desktop.json` and `boxcutter/tpl/vagrantfile-ubuntu1904-desktop.tpl` which you can copy over to your clone of boxcutter to build the base box.

```
git clone https://github.com/boxcutter/ubuntu.git
cp -a boxcutter/ubuntu1904-desktop.json ubuntu/
cp -a boxcutter/tpl/vagrantfile-ubuntu1904-desktop.tpl ubuntu/tpl/
cd ubuntu
packer build -only=virtualbox-iso -var-file=ubuntu1904-desktop.json ubuntu.json
vagrant box add --name ubuntu/1904-desktop box/virtualbox/ubuntu1904-desktop-0.1.0.box
```

# Startup

Starting up the environment is easy.

```
vagrant up
```

# Ansible

Ansible is included in this repository for vagrant to utilize the `ansible_local` provisioner to manage the system configuration.  External roles are added as submodules.  All roles are added to the `type-vagrant.yml` playbook which is the default playbook vagrant will run (defined in the Vagrantfile)

```
git submodule update --init --recursive
```

## External Role Reference

[geerlingguy.pip](https://galaxy.ansible.com/geerlingguy/pip)

[geerlingguy.docker](https://galaxy.ansible.com/geerlingguy/docker)


## Know Issues

If you are using a Windows host, you may run into an issue with file formats
for the ansible templates and files.  If this happens, be sure that you are
using unix style line endings.  i.e. in vim:

```
set ff=unix
```
