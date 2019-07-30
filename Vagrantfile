#Vagrantfile
#$deps_install = <<SCRIPT
#echo Installing Dependencies...
#sudo apt-get update
#sudo apt-get -y dist-upgrade
#sudo apt-get -y install git unzip
##UBUNTU
#echo "[SeatDefaults]
#greeter-session=unity-greeter
#user-session=vagrant
#autologin-user=vagrant
#autologin-user-timeout=0" > /etc/lightdm/lightdm.conf
#systemctl stop lightdm
#systemctl start lightdm
##GNOME
#sed -i 's/\#\ \ AutomaticLogin/\ \ AutomaticLogin/g' /etc/gdm3/custom.conf
#sed -i 's/user1/ubuntu/g' /etc/gdm3/custom.conf
#systemctl restart gdm
#echo "joydev" >> /etc/modules
#SCRIPT

#$userland_install = <<SCRIPT
#sudo -u vagrant virtualenv ~/venv
#sudo -u vagrant virtualenv --python=python3 ~/venv3
#virtualenv --python=python2 ~/venv2
#virtualenv --python=python3 ~/venv3
#if [ -d ~/ubdesktop-Setup ]; then
#  echo "ubdesktop-Setup found, updating"
#  cd ~/ubdesktop-Setup/ &&
#  git pull
#else
#  echo "ubdesktop-Setup not found, cloning"
#  git clone --depth=1 https://github.com/ubdesktop/ubdesktop-Setup.git &&
#  cd ~/ubdesktop-Setup/ &&
#  sudo ./ubdesktop_packages.sh setup basic_install 
#fi
#SCRIPT

Vagrant.configure('2') do |config|

  #vm_box = 'ubuntu/zesty64'
  #vm_box = 'ubuntu/1804-desktop'
  vm_box = 'ubuntu/1904-desktop'
  #config.ssh.private_key_path = ['./.vagrant/ssh/vagrant_rsa']
  #config.ssh.insert_key = false
  #config.ssh.forward_agent = true

  #provisioner = Vagrant::Util::Platform.windows? ? :guest_ansible : :ansible

  config.vm.define :ubdesktop, primary: true  do |ubdesktop|
    ubdesktop.vm.box = vm_box
    ubdesktop.vm.box_check_update = true
    ubdesktop.vm.network "public_network"
    #ubdesktop.vm.network :forwarded_port, guest: 22, host: 22000
    ubdesktop.vm.hostname = "ubdesktop"
    #ubdesktop.vm.synced_folder ".", "/vagrant"
    #ubdesktop.vm.synced_folder "./cloud", "/cloud"
    #ubdesktop.vm.synced_folder "f:/games/emulators", "/home/vagrant/emulators"
    #ubdesktop.vm.provision "file", source: ".vagrant/ssh/vagrant_rsa.pub", destination: "~/.ssh/authorized_keys"
    #ubdesktop.vm.provision "shell", inline: $deps_install, privileged: true
    #ubdesktop.vm.provision "shell", inline: $userland_install, privileged: false
    ubdesktop.vm.provider "virtualbox" do |vb|
      vb.name = "ubdesktop"
      vb.memory = "8192"
      vb.cpus = 2
      vb.customize [ "modifyvm", :id, "--vram", "256" ]
      vb.customize [ "modifyvm", :id, "--accelerate3d", "on" ]
      vb.customize [ "modifyvm", :id, "--usb", "on", "--usbxhci", "on" ] #USB3
      #vb.customize [ "modifyvm", :id, "--usb", "on", "--usbehci", "on" ] #USB2
    end
    ubdesktop.vm.provision "ansible_local" do |ansible|
    #    ansible.verbose = "v"
        ansible.become = true
        ansible.playbook = "ansible/playbooks/type-vagrant.yml"
        ansible.galaxy_roles_path = "/vagrant/ansible/roles"
    end
  end


end
