# Ansible
## Required Packages
- ansible-galaxy collection install community.network
- ansible-galaxy collection install ansible.posix
- ansible-galaxy collection install community.kubernetes
- ansible-galaxy collection install community.general

## Create password file
- touch ~/pw
- echo 'my_vault_password' > ~/pw
## Encrypt passwords
- ansible-vault encrypt_string --name 'pi_password'
- ansible-vault encrypt_string --name 'ubuntu_password'
- ansible-vault encrypt_string --name 'ubnt_password'
- ansible-vault encrypt_string --name 'manjaro_password'
- ansible-vault encrypt_string --name 'ansible_become_pass'
## Read password
- ansible localhost -m ansible.builtin.debug -a var="ansible_become_pass"


ansible-playbook ds.yml -l k8s_workers,k8s_masters

# Recovery
## Control Plane
Desired state: Unplug usb disk drive and shutdown KVM switch
- ansible-playbook ssh.yml -l control_plane -e clean=true
- ansible-playbook ds.yml -l control_plane
- ansible-playbook main.yml -l control_plane -e clean=true
## Node
#### Single node
- ansible-playbook ssh.yml -l c1-node3 -e clean=true
- ansible-playbook ds.yml -l c1-node3
- ansible-playbook main.yml -l c1-node3 -e clean=true -t os
#### All nodes
- ansible-playbook ssh.yml -l k8s_workers -e clean=true
- ansible-playbook ds.yml -l k8s_workers
- ansible-playbook main.yml -l k8s_workers -e clean=true -t os
#### Single master
- ansible-playbook ssh.yml -l c1-master1 -e clean=true
- ansible-playbook ds.yml -l c1-master1
- ansible-playbook main.yml -l c1-master1 -e clean=true -t os
#### All masters
- ansible-playbook ssh.yml -l k8s_masters -e clean=true
- ansible-playbook ds.yml -l k8s_masters
- ansible-playbook main.yml -l k8s_masters -e clean=true -t os