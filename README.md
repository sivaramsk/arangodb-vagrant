# arangodb-vagrant
Setup Arangodb using vagrant in a minute

1. Checkout the project
2. Edit the vagrant file with the right interface and correct ip in the below line ```node.vm.network "public_network", ip: "192.168.0.#{20+machine_id}", bridge: "wlo1"```
3. vagrant up

The anible role can be independetly used without vagrant. 
1. Checkout the project.
2. Edit the hosts.yaml file with the correct ip and groups.
3. ansible-playbook -i hosts.yaml playbook.yaml

The ansible-role is generic and should work on all the linux versions, it has been primarily tested with ubuntu 20.04

