# Install software to the Ansible managed nodes

Specify the packages to be installed and ports to be opened in the config_file.yml.

Assumption: 
1) This playbook only works for debian-based OS.
2) Oracle JDK license has changed and now it requires logging in to an Oracle account to download the pakages. Hence, for the purpose of this assignment, OpenJDK-11 is used instead.
