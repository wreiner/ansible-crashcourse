### Play

- are the primary way to describe automation workflows in Ansible
- defines a set of tasks/roles to be executed on one or more (remote) hosts
- 

#### Example play - Webservers inline tasks

```
---
# ansible-playbook -i inventory/preproduction/hosts.yml webservers.yml -u centos
- name: Install Apache web server
  hosts: webserver
  become: yes

  tasks:
    - name: Install webserver
      dnf:
        name: httpd
        state: present
```

#### Example play - Webservers

```
$ cat webservers.yml
---
# ansible-playbook -i inventory/preproduction/hosts.yml webservers.yml -u centos
- hosts: webservers
  become: yes

  roles:
    - common
    - nginx
```

#### Example play - Database Servers

```
$ cat databaseservers.yml
---
# ansible-playbook -i inventory/preproduction/hosts.yml databaseservers.yml -u centos
- hosts: databases
  become: yes

  roles:
    - common
    - mariadb
```
