# consul-dnsmasq

Installs and Configures [Hasicorp's Consul] (https://consulproject.io) cluster with DNSMasq.



## Inventory

```
[consul-servers]
consulServer1.local
consulServer2.local
consulServer3.local

[consul-bootstrap]
consulBootstrap1.local
consulBootstrap2.local

[consul-clients]
consulClient1.local
consulClient2.local
consulClient3.local
consulClient4.local
consulClient5.local
```

### Encryption Key Generation

```
$ consul keygen
```

## Role Variables

```yml
consul_datacenter: central
consul_uid: 1050
consul_user: consul
consul_group: consul
consul_iface: eth1
consul_ip: 127.0.0.1
consul_log_level: info
consul_port: 8600
consul_suffix: consul
consul_ui_dir: /var/consul/ui
consul_version: 0.5.2
consul_encrypt_key: 2M2aASKoKGek05TjpHcsuw==

```

## Example Playbook

```yml
---
  - hosts:
      - consul-bootstrap
      - consul-servers
      - consul-clients
    sudo: no
    gather_facts: true

    roles:
      - { role: marcelocorreia.apt, tags: ['install','apt'], sudo: true, when: "ansible_system == 'Linux'"}
      - { role: marcelocorreia.consul-dnsmasq, tags: ['install','hashicorp','consul', 'dnsmasq','config']}



    vars_files:
      - /some_path/vars/consul.yml

    vars:
      consul_datacenter: batcave
      consul_uid: 1050
      consul_user: consul
      consul_group: consul
      consul_iface: eth1
      consul_ip: 127.0.0.1
      consul_log_level: info
      consul_port: 8600
      consul_suffix: consul
      consul_ui_dir: /var/consul/ui
      consul_version: 0.5.2
      consul_encrypt_key: 2M2aASKoKGek05TjpHczuw==
```

## Testing

Using this small Vagrant cluster

```Vagrantfile
# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure('2') do |config|
  config.vm.provision 'shell', inline: 'echo Ansible Consul POC'

  config.vm.define 'consulBootstrap1' do |consulBootstrap1|
    consulBootstrap1.vm.box = 'ubuntu/trusty64'
    consulBootstrap1.vm.box_url = '.'
    consulBootstrap1.vm.hostname = 'consulBootstrap1'
    consulBootstrap1.vm.network 'public_network', bridge: "eth1"
    consulBootstrap1.vm.provider 'virtualbox' do |vb|
      # vb.gui = true
      vb.memory = '512'
      vb.cpus = 1
    end
  end

  config.vm.define 'consulBootstrap2' do |consulBootstrap2|
    consulBootstrap2.vm.box = 'ubuntu/trusty64'
    consulBootstrap2.vm.box_url = '.'
    consulBootstrap2.vm.hostname = 'consulBootstrap2'
      consulBootstrap2.vm.network 'public_network', bridge: "eth1"
    consulBootstrap2.vm.provider 'virtualbox' do |vb|
      # vb.gui = true
      vb.memory = '512'
      vb.cpus = 1
    end
  end

  config.vm.define 'consulServer1' do |consulServer1|
    consulServer1.vm.box = 'ubuntu/trusty64'
    consulServer1.vm.box_url = '.'
    consulServer1.vm.hostname = 'consulServer1'
    consulServer1.vm.network 'public_network', bridge: "eth1"
    consulServer1.vm.provider 'virtualbox' do |vb|
      # vb.gui = true
      vb.memory = '512'
      vb.cpus = 1
    end
  end

  config.vm.define 'consulServer2' do |consulServer2|
    consulServer2.vm.box = 'ubuntu/trusty64'
    consulServer2.vm.box_url = '.'
    consulServer2.vm.hostname = 'consulServer2'
    consulServer2.vm.network 'public_network', bridge: "eth1"
    consulServer2.vm.provider 'virtualbox' do |vb|
      # vb.gui = true
      vb.memory = '512'
      vb.cpus = 1
    end
  end

  config.vm.define 'consulServer3' do |consulServer3|
    consulServer3.vm.box = 'ubuntu/trusty64'
    consulServer3.vm.box_url = '.'
    consulServer3.vm.hostname = 'consulServer3'
    consulServer3.vm.network "public_network", bridge: "eth1"
    consulServer3.vm.provider 'virtualbox' do |vb|
      # vb.gui = true
      vb.memory = '512'
      vb.cpus = 1
    end
  end

  config.vm.define 'consulClient1' do |consulClient1|
    consulClient1.vm.box = 'ubuntu/trusty64'
    consulClient1.vm.box_url = '.'
    consulClient1.vm.hostname = 'consulClient1'
    consulClient1.vm.network 'public_network', bridge: "eth1"
    consulClient1.vm.provider 'virtualbox' do |vb|
      # vb.gui = true
      vb.memory = '512'
      vb.cpus = 1
    end
  end

  config.vm.define 'consulClient2' do |consulClient2|
    consulClient2.vm.box = 'ubuntu/trusty64'
    consulClient2.vm.box_url = '.'
    consulClient2.vm.hostname = 'consulClient2'
    consulClient2.vm.network 'public_network', bridge: "eth1"
    consulClient2.vm.provider 'virtualbox' do |vb|
      # vb.gui = true
      vb.memory = '512'
      vb.cpus = 1
    end
  end
end
```

License
-------

MIT

Author Information
------------------

Some useful stuff at:
- [https://github.com/marcelocorreia](https://github.com/marcelocorreia)
- [https://galaxy.ansible.com/list#/users/15516](https://galaxy.ansible.com/list#/users/15516)
- [https://hub.docker.com/u/marcelocorreia/](https://hub.docker.com/u/marcelocorreia/)
- Any issues, pull-request are welcome
# nomad-config
