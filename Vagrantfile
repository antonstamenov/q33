# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "homeserver" do |q33|
     q33.vm.box = "generic/freebsd12"
     q33.vm.hostname = "q33"
  end

  config.vm.provider "parallels" do |prl|
    prl.name = "q33"
    prl.memory = 8096
    prl.cpus = 2
    prl.check_guest_tools = false
  end

  config.vm.network "public_network",  bridge: "en0"

  # config.vm.synced_folder "../data", "/vagrant_data"
  
  config.vm.provision "shell", inline: <<-SHELL
    sed -i'' -e '/firstboot/ d' /etc/rc.conf
    sysrc firstboot_growfs_enable=YES
    sysrc firstboot_pkgs_enable=YES
    sysrc firstboot_pkgs_list="python27"
    touch /firstboot
  SHELL

  config.vm.provision :reload

  config.vm.provision "ansible" do |ansible|
     ansible.playbook = "q33.yml"
  end
end
