
ansible-galaxy collection install community.network
ansible-galaxy collection install ansible.posix
ansible-galaxy collection install community.kubernetes

touch ~/pw
echo 'my_vault_password' > ~/pw 
ansible-vault encrypt_string --name 'pi_password'
ansible-vault encrypt_string --name 'ubuntu_password'
ansible-vault encrypt_string --name 'ubnt_password'
ansible-vault encrypt_string --name 'pi_password'
ansible-vault encrypt_string --name 'pi_password'
ansible-vault encrypt_string --name 'pi_password'
