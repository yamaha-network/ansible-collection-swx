# Ansible collection for Yamaha SWX series

## Modules
The following Ansible modules are part of this collection.

- swx_command.py - Run commands on remote Yamaha SWX devices
- swx_config.py - Manage the configuration of Yamaha SWX devices

## Installation
To install the latest version of this collection, please use the following command:

`ansible-galaxy collection install yamaha_network.swx`

## Requirements
- Ansible 2.10

## Sample playbook 

```
---
- hosts: SWX3100
  connection: network_cli

  tasks:
  - name: get configuration
    yamaha_network.swx.swx_command:
      commands: 
        - show running-config
    register: result

  - name: debug
    debug:
      msg: "{{ result.stdout_lines[0] }}"

  - name: set interface description
    yamaha_network.swx.swx_config:
      lines: 
        - description test
      parents:
        - interface port1.1

  vars:
    ansible_network_os: yamaha_network.swx.swx
    ansible_user: username
    ansible_ssh_pass: password
    ansible_become: true
    ansible_become_password: become_password
```

## Licence

See the LICENSE file.