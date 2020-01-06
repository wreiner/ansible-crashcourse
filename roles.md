### Roles

- Group all items necessary to perform a specific purpose
    - Tasks, defaults, templates, files, etc.
    - Install and configure a webserver
- Should be as small as possible
- Should only perform a specific purpose
    - A wordpress role should only install wordpress and not a database and a webserver too
        - Which database? mariadb, postgresql
        - Which webserver? apache, ngnix
    - Able to build the stack to your needs

#### Tree of a role

```
# geerlingguy/ansible-role-nginx/
# https://github.com/geerlingguy/ansible-role-nginx
ansible-role-nginx/
├── defaults
│   └── main.yml
├── handlers
│   └── main.yml
├── tasks
│   ├── main.yml
│   ├── setup-Archlinux.yml
│   ├── setup-Debian.yml
│   ├── setup-FreeBSD.yml
│   ├── setup-OpenBSD.yml
│   ├── setup-RedHat.yml
│   ├── setup-Ubuntu.yml
│   └── vhosts.yml
├── templates
│   ├── nginx.conf.j2
│   ├── nginx.repo.j2
│   └── vhost.j2
└── vars
    ├── Archlinux.yml
    ├── Debian.yml
    ├── FreeBSD.yml
    ├── OpenBSD.yml
    └── RedHat.yml
```

#### Parts of a role

- main.yml
    - Main entry point for this part of the role
- defaults
    - Holds default values for variables used in the role
- handlers
    - Tasks can call handlers
    - Handlers are run at the end of a playrun
    - Typically restarting services
- tasks
    - The actual tasks which should be performed
    - Calls the modules with the respective parameters
- files
    - Static files which can be copied to the remote host
- templates
    - Templates contain placeholders which are replaced with variable values upon run
    - [jinja template syntax](https://docs.ansible.com/ansible/latest/user_guide/playbooks_templating.html)
- vars
    - Variables which are needed in the role
    - Typically distribution dependend variable values, like package names
        - Apache package
            - Debian: apache2
            - RedHat: httpd
