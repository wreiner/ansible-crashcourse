## Ansible

### What is Ansible?

- Serverless

### Ansible nomenclature

1. YAML
1. Inventory
1. Modules
1. Roles
1. Tasks
1. Playbook

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
