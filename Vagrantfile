# -*- mode: ruby -*-
# vi: set ft=ruby :

# VM array
virt_machines=[
  {
    :hostname => "zabbixagent1",
    :ip => "192.168.0.20"
  },
  {
    :hostname => "zabbixagent2",
    :ip => "192.168.0.21"
  }
]

# Show VM GUI
HOST_SHOW_GUI = false 

# VM RAM
HOST_MEMMORY = "512" 

# VM vCPU
HOST_CPUS = 1

# Network adapter to bridge
#HOST_BRIDGE = "Intel(R) Ethernet Connection (2) I219-V" 
HOST_BRIDGE = "Intel(R) Wireless-AC 9560"

# Which box to use
HOST_VM_BOX = "generic/ubuntu2004" 

################################################
# Parameters passed to provision script
################################################

# Script to use while provisioning
HOST_CONFIIG_SCRIPT = "zabbix-agent.sh" 

# Additional user
HOST_USER = 'test'

# Additional user pass. Root pass will be same
HOST_USER_PASS = '123456789' 

# Run apt dist-upgrade
HOST_UPGRADE = 'false' 

ZABBIX_SERVER_IP = '192.168.0.138'

Vagrant.configure("2") do |config|
	virt_machines.each do |machine|
		config.vm.box = HOST_VM_BOX
		config.vm.define machine[:hostname] do |node|
			node.vm.hostname = machine[:hostname]
			node.vm.network :public_network, bridge: HOST_BRIDGE, ip: machine[:ip]
			node.vm.provider "virtualbox" do |current_vm, override|
				current_vm.name = machine[:hostname]
				current_vm.gui = HOST_SHOW_GUI
				current_vm.memory = HOST_MEMMORY
				current_vm.cpus = HOST_CPUS
				override.vm.provision "shell", path: 'zabbix-agent.sh', args: [	'test', 	'123456789',	'false', 	machine[:hostname], 	machine[:ip],	'192.168.0.138'], run: "once"
			end
		end
	end
end