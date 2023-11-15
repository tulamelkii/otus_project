# -*- mode: ruby -*-
# vim: set ft=ruby

MACHINES = {

:haproxy => {
        :box_name => "tulamelkii/VDebian12",
        :box_version => "12.2.7",
        :vm_name => "haproxy",
        :net => [
          {ip: '192.168.2.1', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "int_1"},
          {ip: '192.168.3.1', adapter: 3, netmask: "255.255.255.252", virtualbox__intnet: "int_2"},
          {ip: '192.168.4.1', adapter: 4, netmask: "255.255.255.252", virtualbox__intnet: "int_3"},

          {ip: '192.168.56.10', adapter: 5},

                ]
 },

:node1 => {
        :box_name => "tulamelkii/VDebian12",
        :box_version => "12.2.7",
        :vm_name => "node1",
        :net => [
                   {ip: '192.168.2.2', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "int_1"},

                  {ip: '192.168.56.11', adapter: 3},
       
                ]
  },

:node2 => {
        :box_name => "tulamelkii/VDebian12",
        :box_version => "12.2.7",
        :vm_name => "node2",
        :net => [
                   {ip: '192.168.3.2', adapter: 2 , netmask: "255.255.255.252", virtualbox__intnet: "int_2"},
                   {ip: '192.168.56.12', adapter: 3},

                ]
},

:barman => {
        :box_name => "tulamelkii/VDebian12",
        :box_version => "12.2.7",
        :vm_name => "barman",
        :net => [
                   {ip: '192.168.4.2', adapter: 2 , netmask: "255.255.255.252", virtualbox__intnet: "int_3"},
                   {ip: '192.168.56.13', adapter: 3},

                ]
},


}
Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|
    
    config.vm.define boxname do |box|
   
      box.vm.box = boxconfig[:box_name]
      box.vm.host_name = boxconfig[:vm_name]
      box.vm.box_version = boxconfig[:box_version]
      boxconfig[:net].each do |ipconf|
      box.vm.network "private_network", ip: ipconf[:ip], virtualbox__intnet: ipconf[:virtualbox__intnet], netmask: ipconf[:netmask], adapter: ipconf[:adapter]
      end
       box.vm.provider :virtualbox do |v|
        v.customize ['modifyvm', :id, '--nested-hw-virt', 'on']
      end

  
# if boxconfig[:vm_name] == "barman"
#       box.vm.provision "ansible" do |ansible|
#        ansible.playbook = "main.yml"
#        ansible.inventory_path = "host"
#        ansible.host_key_checking = "false"
#        ansible.limit = "all"
#         end
#       end
    end
  end
end
