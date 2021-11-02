# arangodb-vagrant
Setup Arangodb using vagrant in a minute

1. Checkout the project
2. Edit the vagrant file with the right interface and correct ip in the below line 
   * __node.vm.network "public_network", ip: "192.168.0.#{20+machine_id}", bridge: "wlo1"__
   * Private interface(Host-only adapter) does not seem to work. Use public_network here and make sure the ip subnet matches your DHCP. 
4. vagrant up

The anible role can be independetly used without vagrant. 
1. Checkout the project.
2. Edit the hosts.yaml file with the correct ip and groups.
3. ansible-playbook -i hosts.yaml playbook.yaml

Sample playbook.yaml

```
127.0.0.1 ansible_connection=local

[agents]
192.168.0.20 ansible_user=vagrant 
192.168.0.21 ansible_user=vagrant
192.168.0.22 ansible_user=vagrant

[dbservers]
192.168.0.23 ansible_user=vagrant 
192.168.0.24 ansible_user=vagrant
192.168.0.25 ansible_user=vagrant

[coordinators]
192.168.0.26 ansible_user=vagrant 
192.168.0.27 ansible_user=vagrant
192.168.0.28 ansible_user=vagrant
```

Keep the 127.0.0.1 in the above as it is used to create credentials locally. Replace the ip's appropriately. 

The ansible-role is generic and should work on all the linux versions, it has been primarily tested with ubuntu 20.04

