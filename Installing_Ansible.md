### Install Ansibile

1. Create instance with AMI = 20.04 lts
2. Connect via SSH to Gitbash terminal
3. Run commands: `sudo apt update`
4. `sudo apt upgrade -y`
5. *`sudo apt install software-properties-common`*: Installs the `software-properties-common` package, which provides scripts for managing software repositories. This is a prerequisite for adding the Ansible repository.
6. *`sudo apt-add-repository ppa:ansible/ansible`*: Adds the Ansible Personal Package Archive (PPA) to your list of sources. This ensures that you can install Ansible directly from this source.
7. *`sudo apt update -y`*: Updates the local package cache to make sure you have the latest list of packages from all repositories, including the recently added Ansible PPA.
8. *`sudo apt install ansible -y`*: Installs the Ansible software package.
9. *`ansible --version`*: Checks the installed version of Ansible.

### Inside Ansible
1. *`cd /etc/ansible/`*: Navigates to the `/etc/ansible/` directory, where Ansible's global configuration and inventory files are typically located.
2. *`sudo apt install tree`*: Installs the `tree` utility, which is used for directory visualization.
3. *`tree`*: Runs the `tree` command to display a tree view of the directory structure. In this case, you would be seeing the structure of the `/etc/ansible/` directory.

#### SSH
1. Open a new second Gitbash terminal
1. Make sure your in the home directory `cd`
2. Run command *`scp -i "/.ssh/tech254.pem" ~/.ssh/tech254.pem ubuntu@ec2-34-250-136-251.eu-west-1.compute.amazonaws.com:/.ssh`*: Copies your local `.pem` file (`tech254.pem`) to a remote machine via SSH. The `-i` option specifies the key to use for the operation.
**NOTE: change IP address for your instance**
   - Source: `~/.ssh/tech254.pem`
   - Destination: `ubuntu@ec2-34-250-136-251.eu-west-1.compute.amazonaws.com:~/.ssh`
   
4. *`cd .ssh` back to ssh folder 
5. ls to check if it's `tech254.pem`

#### Connecting to different instance
1. 
```
# inventory.ini
[my_instance]
34.245.20.82 ansible_ssh_private_key_file=~/.ssh/tech254.pem ansible_ssh_user=ubuntu
```
NOTE: IP ADDRESS IS DEPENDANT ON WHICH instance you want to connect.

```
chmod 400 ~/.ssh/tech254.pem

ansible -i inventory.ini my_instance -m ping

nano my_playbook.yml
```

Copy and paste:
```
---
- name: My Ansible Playbook
  hosts: my_instance
  tasks:
    - name: Echo a message
      command: echo "Hello, Ansible!"
```
`ansible-playbook -i inventory.ini my_playbook.yml`s