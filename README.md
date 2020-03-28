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
## Installation Configuration
1) There are 2 variable files namely `config_file_RedHat.yml` and `config_file_Ubuntu.yml`. As the name implies, these are the configuration files for the software installation on RedHat a Ubuntu respectively.
2) In this assignment, Apache, Tomcat, MySQL services are required and the tcp ports of 80, 8080, and 3306 must be opened to allow the access to the respective services.
3) There are a few utilities namely telnet, curl, nslookup and Oracle JDK (OpenJDK is used instead) required to support the tasks indicated.
4) The challenge is that the package name of the same service/utility could be different between Ubuntu and Redhat. Hence, there are 2 variable files defining the diffent package names for the services.

## Run the playbook!
1) The last step is to run the playbook. In the `main.yml` file, Ansible will first gather facts about the managed nodes and it will intelligently identify the Linux distro of the manage nodes so there is no need to modify anything in the `main.yml` file.
2) To run the playbook, simply type `$ ansible-playbook main.yml` and the installation will start immeditely. The playbook output is stored in `ansible_play_output.txt` for referencce.

Lastly, refer to `deliverables.txt` for the output of the commands accessing the installed services. Enjoy!
