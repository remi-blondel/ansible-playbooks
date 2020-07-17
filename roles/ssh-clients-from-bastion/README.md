ssh-clients-from-bastion
=========

This role does not contain much tasks, but is used to test an ssh/ansible configuration using a host as bastion to proxy the ssh connection.
This is done through ssh multiplexing.

More info here: https://blog.scottlowe.org/2015/12/24/running-ansible-through-ssh-bastion-host/

Network Diagram
--------------

![alt text](https://raw.githubusercontent.com/remi-blondel/ansible-playbooks/master/roles/check-net-config/network_diagram.png)

SSH Configuration:
----------------

```bash
Host 10.0.2.1
  ProxyCommand ssh -W %h:%p 172.16.1.1
  IdentityFile ~/.ssh/id_rsa_client1

Host 10.0.3.1
  ProxyCommand ssh -W %h:%p 172.16.1.1
  IdentityFile ~/.ssh/id_rsa_client1

Host 172.16.1.1
  Hostname 172.16.1.1
  User root
  IdentityFile ~/.ssh/id_rsa
  ControlMaster auto
  ControlPath ~/.ssh/ansible-%r@%h:%p
  ControlPersist 5m
```
*located in `~/.ssh/ssh.cfg`

Ansible Configuration:
----------------

```bash
[ssh_connection]
ssh_args = -F /root/.ssh/ssh.cfg -o ControlMaster=auto -o ControlPersist=30m
control_path = ~/.ssh/ansible-%%r@%%h:%%p
```
* located in `/etc/ansible/ansible.cfg`