# Network Pi
An Ansible playbook that configures a Raspberry Pi running Ubuntu Server 22.04 as a home network manager.

## Prerequisites
This playbook assumes you have a server running Ubuntu Server 22.04 with a user that has `sudo` privileges.

## Roles

It uses the following [geerlingguy](https://galaxy.ansible.com/geerlingguy) Ansible roles to the setup of some defaults:

| Role | Description |
| ---- | ----------- |
| geerlingguy.security | Some sane security defaults |
| geerlingguy.firewall | A basic firewall |
| geerlingguy.pip | The python package manager (used to install docker) |
| geerlingguy.docker | Setups up Docker |

This playbook also has the following roles:

| Role | Description |
| ---- | ----------- |
| pihole | A blackhole DNS (docker container) |
| unbound | A recursive DNS (docker container) |
| unifi controller | A network controller (docker container) |

## Configuration
- Configurable defaults can be found in the `group_vars/all/main.yml` file.
- Host specific variables should be defined in `host_vars/network-pi`.

## Usage
- Install third-party roles from `requirements.txt`: `ansible-galaxy role install -r requirements.yml`
- Create `.../host_vars/networkpi/vars.yml` with varible overrides for the empty variables in `.../group_vars/all/vars.yml` 
- Create the `hosts` inventory file with the following
    ```ini
    [networkpi]
    <ip> 

    [networkpi:vars]
    ansible_host=
    ansible_port=
    ansible_user=
    ansible_connection=ssh
    ansible_private_key_file=~/.ssh/private_key
    ```
- Run `ansible-playbook main.yml -K`