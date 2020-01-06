### Inventory

#### Overview

- Holds and groups all available inventory items
    - Hostgroups and their hosts
    - Group variables - *group_vars*
        - Variables which are available for all hosts of this group
        - Special *all.yml* which are available for all hosts in all groups
    - Host variables - *host_vars*
        - Variables specifically for individual hosts

#### Complex but meaningful inventory example

```
# directory structure
inventory/
├── preproduction
│   ├── group_vars
│   │   └── all.yml
│   ├── host_vars
│   │   ├── mail01tst.yml
│   │   └── mon01tst.yml
│   └── hosts.yml
└── production
    ├── group_vars
    │   └── all.yml
    ├── hosts.yml
    └── host_vars
        ├── www01.yml
        ├── mail01.yml
        ├── mon01.yml
```

#### Starting point is hosts.yml

```
---
# inventory/production/hosts.yml
mailservers:
  hosts:
    mail01:

webservers:
  hosts:
    www01:

monitoring:
  hosts:
    mon01:
```

#### Catchall group variables

```
---
# inventory/production/group_vars/all.yml

# ssh public keys of all admins
admin_ssh_public_keys: |
  ssh-rsa ...
  ssh-dsa ...

# sshd
sshd_allowtcpforwarding: "yes"
sshd_passwordauthentication: "yes"
sshd_x11forwarding: "no"
```

#### Host specific variables

```
# inventory/production/host_vars/www01.yml

wordpress__install_directory: "/var/www"
```