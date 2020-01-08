## Ansible Crash Course

Onboarding crash course for Ansible.

### What is Ansible?

- IT automation tool
- Agentless
- Uses ssh for transport

### Ansible nomenclature

1. YAML
1. [Inventory](inventory.md)
1. Modules
1. [Roles](roles.md)
1. Tasks
1. [Playbook](play.md)
1. [Vault](vault.md)
1. [Ansible Galaxy](ansible-galaxy.md)

### Video Course

- [The Cloud Coach - Ansible Crash Course](https://www.thecloud.coach/ansible-crash-course)

### What we are about to setup

- Two VMs in an virtualization environment
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
