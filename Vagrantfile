Vagrant.configure('2') do |config|

  #vm_box = 'blueflame/ubuntu2004-desktop'
  #vm_box_version = '20201205.1'
  vm_box = 'blueflame/ubuntu2004.live-desktop'
  vm_box_version = '20201205.1-live'


  config.vm.define :ubdesktop, primary: true  do |ubdesktop|
    ubdesktop.vm.box = vm_box
    ubdesktop.vm.box_check_update = true
    ubdesktop.vm.network "public_network"
    ubdesktop.vm.hostname = "ubdesktop"
    ubdesktop.vm.provider "virtualbox" do |vb|
      vb.name = "ubdesktop"
      vb.memory = "4096"
      vb.cpus = 2
      vb.customize [ "modifyvm", :id, "--vram", "64" ]
      vb.customize [ "modifyvm", :id, "--accelerate3d", "on" ]
      vb.customize [ "modifyvm", :id, "--graphicscontroller", "vmsvga" ]
      vb.customize [ "modifyvm", :id, "--usb", "on", "--usbxhci", "on" ] #USB3
    end
    ubdesktop.vm.provision "ansible" do |ansible|
        ansible.verbose = "v"
        ansible.config_file = "ansible/ansible.cfg"
        ansible.become = true
        ansible.playbook = "ansible/playbooks/type-vagrant.yml"
        ansible.galaxy_roles_path = "ansible/roles"
    end
  end


end
