Vagrant.configure("2") do |config|

  config.ssh.insert_key = false
  
  config.vm.provider :virtualbox do |vb|
   vb.memory = 4096
   vb.cpus = 2
  end

  #Disabling the default /vagrant share
  config.vm.synced_folder ".", "/vagrant", disabled: false
  MACHINE = ["arango1","arango2","arango3"]
  N = 2

  (0..N).each do |machine_id|
    config.vm.define "server#{machine_id}" do |node|
      node.vm.hostname = MACHINE[machine_id]
      node.vm.box = "generic/ubuntu2004"
      node.vm.network "public_network", ip: "192.168.0.#{20+machine_id}", bridge: "wlo1"

    
      if machine_id == N
        node.vm.provision :ansible do |ansible|
          ansible.limit = "all"
          ansible.galaxy_roles_path = './ansible/roles'
          ansible.inventory_path = 'hosts.yaml'
          ansible.playbook = 'playbook.yml'
        end
      end    
    end
  end
end
