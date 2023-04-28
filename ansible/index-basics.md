## Ansible Crash Course

Onboarding crash course for Ansible.

### What is Ansible?

- open-source configuration management and automation tool
- automate IT tasks such as provisioning, deployment, and orchestration of software and infrastructure
- agentless architecture
  - it doesn't require any software to be installed on the target hosts
  - easy to deploy and manage
  - connects to remote servers via SSH
- can be used for a wide range of tasks
  - from simple server configuration and application deployment to complex infrastructure management and continuous delivery
- uses a simple, human-readable language called YAML to describe automation jobs

### Ansible nomenclature

1. [YAML](yaml.md)
1. [Inventory](inventory.md)
1. [Playbook](play.md)
1. [Tasks](tasks.md)
1. [Modules](modules.md)
1. [Roles](roles.md)
   1. [Common role](role-common.md)
   1. [nginx role](role-nginx.md)
1. [Variables, conditionals, loops](variables_conditionals_loops.md)
1. [Vault](vault.md)
1. [Ansible Galaxy](ansible-galaxy.md)

- see [Ansible docs](https://docs.ansible.com/ansible/latest/getting_started/basic_concepts.html)

### What we are about to setup

- Two VMs in a virtualization environment
    - One database host with mariadb
    - One nginx host with wordpress
    - All hosts should have vim and tmux installed
    - On all hosts the centos user should have the same authorized_keys

### Step by step

1. Create the inventory
1. Create the play
1. Create common role
    - Install needed packages
        - Variables
        - Loops
        - Conditionals
    - Disallow agent forwarding in ssh
    - Deploy authorized_keys
        - Group variables
        - Host variables
1. Create nginx role
    - Install nginx
    - Enable and start service
    - Deploy index.html
        - Contains ipv4 address of the node
1. Create a [vault](vault.md) for sensible data
1. Create roles for php 7.3 and wordpress
1. Install mariadb with ansible-galaxy
