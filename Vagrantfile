# -*- mode: ruby -*-
# vi: set ft=ruby :

OS="centos/7"

MACHINES = {
   :ns01 => {
      :box_name => OS,
      :vm_name => "ns01",
      :net => [   
                  ["192.168.10.10", 2, "255.255.255.0",  "dns"], 
                  ["192.168.50.10", 8, "255.255.255.0"],
               ]
   },

   :ns02 => {
      :box_name => OS,
      :vm_name => "ns02",
      :net => [   
                  ["192.168.10.11", 2, "255.255.255.0",  "dns"], 
                  ["192.168.50.11", 8, "255.255.255.0"],
               ]
   },

   :client1 => {
      :box_name => OS,
      :vm_name => "client1",
      :net => [   
                  ["192.168.10.15", 2, "255.255.255.0",  "dns"], 
                  ["192.168.50.15", 8, "255.255.255.0"],
               ]
   },

   :client2 => {
      :box_name => OS,
      :vm_name => "client2",
      :net => [   
                  ["192.168.10.16", 2, "255.255.255.0",  "dns"], 
                  ["192.168.50.16", 8, "255.255.255.0"],
               ]
   },
}

Vagrant.configure("2") do |config|
   MACHINES.each do |boxname, boxconfig|
     config.vm.define boxname do |box|
       box.vm.box = boxconfig[:box_name]
       box.vm.host_name = boxconfig[:vm_name]
       
       box.vm.provider "virtualbox" do |v|
         v.memory = 256
         v.cpus = 1
        end
 
       boxconfig[:net].each do |ipconf|
         box.vm.network("private_network", ip: ipconf[0], adapter: ipconf[1], netmask: ipconf[2], virtualbox__intnet: ipconf[3])
       end
 
       box.vm.provision "shell", inline: <<-SHELL
         mkdir -p ~root/.ssh
         cp ~vagrant/.ssh/auth* ~root/.ssh
       SHELL
      #  if boxconfig[:vm_name] == "client2"
      #   config.vm.provision "ansible" do |ansible|
      #    ansible.verbose = "vvv"
      #    ansible.playbook = "playbook.yml"
      #    ansible.become = "true"
      #   end
      #  end
     end
     config.vm.synced_folder '.', '/vagrant', disabled: true
   end
 end


# --------------------------- Old conf ---------------------------------
# Vagrant.configure(2) do |config|
#    config.vm.box = "centos/7"
 
#    # config.vm.provision "ansible" do |ansible|
#    #   ansible.verbose = "vvv"
#    #   ansible.playbook = "provisioning/playbook.yml"
#    #   ansible.become = "true"
#    # end
 
 
#    config.vm.provider "virtualbox" do |v|
#       v.memory = 256
#    end
 
#    config.vm.define "ns01" do |ns01|
#      ns01.vm.network "private_network", ip: "192.168.50.10", netmask: "255.255.255.0", virtualbox__intnet: "dns"
#      ns01.vm.hostname = "ns01"
#      ns01.vm.provision "shell", inline: <<-SHELL
#      mkdir -p ~root/.ssh
#      cp ~vagrant/.ssh/auth* ~root/.ssh
#      SHELL
#    end
 
#    config.vm.define "ns02" do |ns02|
#      ns02.vm.network "private_network", ip: "192.168.50.11", netmask: "255.255.255.0", virtualbox__intnet: "dns"
#      ns02.vm.hostname = "ns02"
#      ns02.vm.provision "shell", inline: <<-SHELL
#      mkdir -p ~root/.ssh
#      cp ~vagrant/.ssh/auth* ~root/.ssh
#      SHELL
#    end
 
#    config.vm.define "client1" do |client1|
#      client1.vm.network "private_network", ip: "192.168.50.15", netmask: "255.255.255.0",  virtualbox__intnet: "dns"
#      client1.vm.hostname = "client1"
#      client1.vm.provision "shell", inline: <<-SHELL
#      mkdir -p ~root/.ssh
#      cp ~vagrant/.ssh/auth* ~root/.ssh
#      SHELL
#    end
 
#    config.vm.define "client2" do |client2|
#      client2.vm.network "private_network", ip: "192.168.50.16", netmask: "255.255.255.0", virtualbox__intnet: "dns"
#      client2.vm.hostname = "client2"
#      client2.vm.provision "shell", inline: <<-SHELL
#      mkdir -p ~root/.ssh
#      cp ~vagrant/.ssh/auth* ~root/.ssh
#      SHELL
#    end
#  end
 