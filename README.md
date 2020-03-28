# Install software to the Ansible managed nodes

Notes: 
1) The Ansible Engine is running on local machine running RedHat OS and is managing the EC2 instance via SSH connection. 
2) Oracle JDK license has changed and now it requires logging in to an Oracle account to download the pakages. Hence, for the purpose of this assignment, OpenJDK-11 is used instead.
3) For Red Hat inventory, the community version of MySQL is MariaDB so the mariadb-server package is used. For Ubuntu inventory, mysql-server package is used.

## SSH to the inventories
1) There are several ways to configure SSH access to the inventories such as 
* Defining the ansible_user and ansible_password in the inventory file (not recommended)
* Saving the credentials as variable and use ansible-vault to encrypt it (recommended but tedious)
* Manually input the credentials upon running the playbook (even more tedious)
* Using SSH keys to connect to the managed inventories without password (**highly recommended**)
2) The easiest and safest way (provided the Ansible host is not compromised) is to set up passwordless SSH connection using SSH keys.
3) To do that, ensure the SSH keys are generated. Otherwise run `$ ssh-keygen -t rsa -b 4096` to generate the SSH keys.
4) After the keys are generated, run `$ ssh-copy-id <username>@<ip address of the target inventory>`. You will be prompt to key in the password for the target inventory.

## Set up the inventory file
1) The inventory file is where the details of the managed nodes are defined.
2) In this case, there's one managed node under the group `ec2` as seen below. There are 2 things need to take note of:
* The IP address must be the Public IP address of the EC2 instance. 
* The `ansible_user` is the user we use to connect to the node via SSH. The name of the user can be found in the AWS console.
```
[ec2]
18.140.245.50 ansible_user=ec2-user
```
## Variables
1) There are 2 variable files namely `config_file_RedHat.yml` and `config_file_Ubuntu.yml`. As the name implies, these are the configuration files for RedHat a Ubuntu 
