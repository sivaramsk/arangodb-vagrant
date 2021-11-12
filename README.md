# arangodb-vagrant
Setup Arangodb cluster using vagrant in a minute. This project sets up arangodb in a cluster configuraiton using ArangoDB starter. 

### Pre-requisites:
1. Virtualbox 
2. Vagrant

### Install Instruction:
1. Checkout the project
2. Check out the arangodb-collection project from https://github.com/sivaramsk/arangodb-collection
3. Edit the vagrant file with the right interface and correct ip in the below line 
   * __node.vm.network "public_network", ip: "192.168.0.#{20+machine_id}", bridge: "wlo1"__
     * Private interface(Host-only adapter) does not seem to work. Use public_network here and make sure the ip subnet matches your DHCP. 
     * If you change the ip in the above configuration, make sure you change the ip values in the playbook.yaml and hosts.yaml.
4. vagrant up

### Configuration Options for arangodb_starter role: 
__Take a look at the sample site.yml provided for configuring separate agents, dbservers and coordinator services__
```
---

arangodb_version: "3.8.2"
arangodb_authentication: false
arangodb_username: "root"
arangodb_password: ""
arangodb_starter_port: 8528
arangodb_agents:
  - 192.168.0.20
  - 192.168.0.21
  - 192.168.0.22
arangodb_servers: # DBServers and Coordinators IP to create TLS. Comment it out if are using only 3 nodes.
  - 192.168.0.23
  - 192.168.0.24
  - 192.168.0.25
  - 192.168.0.26
  - 192.168.0.27
  - 192.168.0.28
  - 192.168.0.29
```



### Sample hosts file for installing agents, dbserver and coordinators seperately. 

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

**Keep the 127.0.0.1 in the hosts.yaml as it is used to create credentials locally. Replace the other ip's appropriately**

The ansible-role is generic and should work on all the linux versions, it has been primarily tested with ubuntu 20.04

