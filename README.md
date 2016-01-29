# nomad-config ![Nomad by Hashicorp](https://www.nomadproject.io/assets/images/logo-header-f33e7fb0.png)

Installs and Configures [Hashicorp's Nomad] (https://nomadproject.io) Cluster.



It uses ansible inventory to configure the whole cluster. Can also be used 
combined with the role [consul-dnsmasq] (https://github.com/marcelocorreia/consul-dnsmasq). 


## Inventory for Nomad alone

```
bootstrap[1:2].local ansible_connection=ssh ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/key.pem
server[1:3].local ansible_connection=ssh ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/key.pem
worker[1:13].local ansible_connection=ssh ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/key.pem
anotherclient.com ansible_connection=ssh ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/key.pem

[nomad-bootstrap]
bootstrap[1:2].local

[nomad-servers]
server[1:3].local

[nomad-clients]
worker[1:21].local
anotherclient.local

```


## Inventory for Nomad + Consul 

```
bootstrap[1:2].local ansible_connection=ssh ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/key.pem
server[1:3].local ansible_connection=ssh ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/key.pem
client[1:13].local ansible_connection=ssh ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/key.pem
anotherclient.com ansible_connection=ssh ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/key.pem

[consul-bootstrap]
bootstrap[1:2].local

[consul-servers]
server[1:3].local

[consul-clients]
worker[1:13].local
anotherclient.local
wholebunchofclients[1:50].whatever.io

[nomad-bootstrap]
bootstrap[1:2].local

[nomad-servers]
server[1:3].local

[nomad-clients]
worker[1:21].local
anotherclient.local

```

### Encryption Key Generation

```
$ consul keygen
```

## Role Variables

```yml
nomad_datacenter: central
nomad_user: root
nomad_group: root
nomad_iface: eth0
nomad_ip: 127.0.0.1
nomad_log_level: info
nomad_port: 8600
nomad_suffix: consul
nomad_ui_dir: /var/consul/ui
nomad_version: 0.5.2
nomad_encrypt_key: 2M2aASKoKGek05TjpHcsuw==

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
