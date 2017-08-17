
# Ansible

## Resource

https://serversforhackers.com/c/an-ansible-tutorial

## Hosts
/etc/ansible/hosts

format:

[group names]

<name>

ex.

[webservers]

example.com

example2.com

## Command 

ansible all -m ping -s -k -u vagrant

    all - Use all defined servers from the inventory file

    -m ping - Use the "ping" module, which simply runs the ping command and returns the results

    -s - Use "sudo" to run the commands

    -k - Ask for a password rather than use key-based authentication

    -u vagrant - Log into servers using user vagrant

### Run shell command

ansible all -s -m shell -a 'apt-get install nginx'

    - a arg


ansible all -s -m apt -a 'pkg=nginx state=installed update_cache=true'

## Playbook

stored in yaml

ex. install nginx

### Tasks

```yaml
---
- hosts: local
  tasks:
   - name: Install Nginx
     apt: pkg=nginx state=installed update_cache=true
```

### Execute a playbook

ansible-playbook -s nginx.yml

### Handler

useful for secondary actions such as starting services

```yaml
handlers:
   - name: Start Nginx
     service: name=nginx state=started
```

## Roles

organizes tasks and data into coherent structure

directory structure:
```
rolename
 - files
 - handlers
 - meta
 - templates
 - tasks
 - vars
```

in each dir is a main.yml

### template dir

Template files contain vars based on python jinja2. Used to define config files etc...

### vars dir

main.yml lists the variables that will be used

### running roles

define where roles are: /etc/ansible/ansible.cfg roles_path = some/dir

create a yaml file to run the role(s)

```yaml
---
- hosts: all
  roles:
    - nginx
```

run the role(s) with 

ansible-playbook -s <yaml file>

## Vault

Used to store sensitive information (vars)

ansible-vault create vars/main.yml

ansible-vault edit vars/main.yml


