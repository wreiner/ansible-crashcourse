### Ansible Vault

- Ansible Vault is a feature of ansible that allows you to keep sensitive data such as passwords or keys in encrypted files, rather than as plaintext in playbooks or roles
    - https://docs.ansible.com/ansible/latest/user_guide/vault.html

#### Whole file as a vault

- Create the vault

```
$ ansible-vault create credentials.yml
```

- Edit the vault

```
$ ansible-vault edit credentials.yml
```

- View the vault

```
$ ansible-vault view credentials.yml
```

#### Use the vault in an ansible run

```
$ ansible-playbook -i inventory/preproduction/hosts.yml --extra-vars="@credentials.yml" databases.yml --ask-vault-pass
```

