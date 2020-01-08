### Ansible Galaxy

- Galaxy is a hub for finding and sharing Ansible content
    - https://galaxy.ansible.com/
- Galaxy provides pre-packaged units of work known to Ansible as Roles

#### Use mariadb module from Galaxy

- Install the package
    - Files will be downloaded to *~/.ansible*

```
$ ansible-galaxy install bertvv.mariadb
```

- Configure the module through inventory

```
# inventory/preproduction/host_vars/anststdb01.yml
# -- bertvv.mariadb
# https://galaxy.ansible.com/bertvv/mariadb
# ansible-galaxy install bertvv.mariadb
mariadb_bind_address: "{{ wordpress__dbhost }}"
mariadb_configure_swappiness: false
mariadb_mirror: "yum.mariadb.org"
mariadb_port: 3306
mariadb_root_password: "mariadb"
mariadb_service: "mariadb"

mariadb_databases:
  - name: "{{ wordpress__dbname }}"

mariadb_users:
  - name: "{{ wordpress__dbuser }}"
    password: "{{ wordpress__dbpassword }}"
    priv: "{{ wordpress__dbname }}.*:ALL"
    host: '%.%'
```

- Use the package in your play

```
- hosts: databases
  become: yes

  roles:
    - common
    - bertvv.mariadb
```
