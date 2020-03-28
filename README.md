# Install software to the Ansible managed nodes

Specify the packages to be installed and ports to be opened in the config_file.yml.

Assumption: 
1) Oracle JDK license has changed and now it requires logging in to an Oracle account to download the pakages. Hence, for the purpose of this assignment, OpenJDK-11 is used instead.

## SSH to the inventories
1) There are several ways to configure SSH access to the inventories such as 
* Defining the ansible_user and ansible_password in the inventory file (not recommended)
* Saving the credentials as variable and use ansible-vault to encrypt it (recommended but tedious)
* Manually input the credentials upon running the playbook (even more tedious)
* Using SSH keys to connect to the managed inventories without password (**highly recommended**)
2) The easiest and safest way (provided the Ansible host is not compromised) is to set up passwordless SSH connection using SSH keys.
3) To do that, ensure the SSH keys are generated. Otherwise run `$ ssh-keygen -t rsa -b 4096` to generate the SSH keys.
4) After the keys are generated, run `$ ssh-copy-id <username>@<ip address of the target inventory>`. You will be prompt to key in the password for the target inventory.

