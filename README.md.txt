Ansible Server and node Setup:
================================
1. Go to AWS acount -> Create 3 EC2 instance in same AZ
2. Now go inside ansible server and download the ansible packages
Download Ansible packages:
=> sudo dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
3. Now do "ls"
=> yum update -y
4. Now install all the packages one by one
=> yum install git python python-level python-pip ansible
5. Now go to hosts file inside ansible server and paste private ip of all nodes
=> vi etc/ansible/hosts
6. Now this hosts file is only working after updating ansible.cfg file
=> vi etc/ansible/ansible.cfg
7. Uncomment/Add the inventory and sudo-user
8. Create one user, in all 3 instances 
=> adduser ansible
9. Set password for the ansible user
=> passwd ansible
10. switch as ansible user
=> su - ansible
11. to give ansible user to sudo priviledge follow the below command
=>visudo
=> root       ALL=(ALL)       ALL
=> ansible    ALL=(ALL)       NOPASSWD:ALL
12. do this 10# and 11# for all nodes
13.To establish the connection with nodes  go to ansible server and need to do changes in sshd-config file
=> vi etc/ssh/sshd-config
14. Do this step 13# for all nodes and restart the sshd service
=> service sshd restart
15. Now verify in ansible server 
=> su - ansible
=> ssh <ip address>
16. Now it will prompt for password
17. Go to ansible server and create keys and run below command as ansible user
=> ssh-keygen
=> ls -a
=> cd .ssh
=> ls
18. Need to copy public key to both the nodes
=> ssh-copy-id ansible@<private_IP_nodes>
19. Verfify and go to ansible server 
=> ansible all --list-hosts
