config-router-3
=========

This role is configuring the following elements on router3:
- IPv4 interfaces configuration
- Routes configuration
- Nat configuration

Requirements
------------

At least one CentOS 8 host acting as a router:
- Enable IP forwarding
- Configure nat with iptables (not firewalld)


Network Diagram
--------------

![alt text](https://raw.githubusercontent.com/remi-blondel/ansible-playbooks/master/roles/check-net-config/network_diagram.png)

Variables
--------------

The playbook is only configuring router3. Modify `main.yml` in role/vars/ accordingly to match your desired router config.

Example Playbook
----------------

```bash
- name: Configure router3
  hosts:
    - router3
  gather_facts: no

  roles:
    - config-router3
```