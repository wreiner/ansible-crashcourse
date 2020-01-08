## Handler

- Handlers are lists of tasks
    - [Ansible documentation](https://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html#handlers-running-operations-on-change)
- Globally unique name
- Will only run when action sends notify

### Example handler

```
- name: "Restart nginx daemon"
  service:
    name: "nginx"
    state: "restarted"
```
