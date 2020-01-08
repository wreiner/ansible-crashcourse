### nginx Role

- Will install nginx packages
- Will deploy nginx config
    - Two phases
- Modules
    - package
    - template
    - file
- Notify and Handlers

#### Tasks

##### Deploy nginx config

- Phase 1 is most basic version
- Phase 2 is for actually using wordpress

- When the config file is modified call the handler
    - *Restart nginx daemon*
    - [Handler](handlers.md)

```
- name: "Deploy nginx.conf"
  template:
    src: "nginx.conf.phase1.j2"
    dest: "/etc/nginx/nginx.conf"
    owner: root
    group: root
    mode: 0644
    backup: "yes"
  notify: "Restart nginx daemon"
```

```
- name: "Deploy nginx.conf"
  template:
    src: "nginx.conf.phase2.j2"
    dest: "/etc/nginx/nginx.conf"
    owner: root
    group: root
    mode: 0644
    backup: "yes"
  notify: "Restart nginx daemon"
```

- Create the handler

```
# roles/nginx/handlers/main.yml
- name: "Restart nginx daemon"
  service:
    name: "nginx"
    state: "restarted"
```
