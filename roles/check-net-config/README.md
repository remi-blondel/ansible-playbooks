check-net-config
=========

This role is checking the following elements:
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

The playbook is only testing the first router's configuration. Modify `interfaces_vars.yml` accordingly to match your own. Playbook will still work if you add more routers or interfaces.


Example Playbook
----------------

```bash
- name: Checking routers network configuration
  hosts:
    - router1
  gather_facts: yes
  roles:
    - check-net-config
```