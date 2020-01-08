### Play

- Tells ansible what to do

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
