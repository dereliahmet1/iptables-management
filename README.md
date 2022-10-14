# iptables-management
This role is managing the iptables persistent installation and making basic configurations on iptables

- Installs dependencies
- Configures services

## Requirements

This role is written for Debian based operating systems.
Ansible version => 2.10

## Note

If you don't have the ssh host key checking configuration in your default config, you can set this environment variable in your machine.

```
export ANSIBLE_HOST_KEY_CHECKING=False

```
 
## Tested On

Ubuntu 14.04 -
Ubuntu 16.04 -
Ubuntu 18.04 -
Ubuntu 20.04 -
Debian 10 -
Debian 9 -

## Tested with 

Ansible Server Version 2.13
Python Version 3.10

## Role Variables

| Variable                  | Required | Default                    |
| ------------------------- | -------- | -------------------------- |
| installation              | yes      | 1                          |
| configuration             | yes      | 1                          |


## Example Playbook

```YAML
- name: Apply Iptables Installation and Rules
  hosts: all
  become: false
  gather_facts: false
  roles:
    
    - role: iptables.install
      when: installation|default(false)|bool
    
    - role: iptables.apply.rules
      when: configuration|default(false)|bool
 
  vars:
    - installation: 0
    - configuration: 1

```

## Example Hosts File

```YAML
[all]
instanceA ansible_ssh_host=10.0.0.1 ansible_ssh_user=root ansible_ssh_pass=passwordA
instanceB ansible_ssh_host=10.0.0.2 ansible_ssh_user=root ansible_ssh_pass=passwordB

[server1]
instanceA

[server2]
instanceB

```