### Common Role

- Will install basic packages
- Will deploy public keys
- Modules
    - package
    - authorized_key
    - lineinfile
    - debug
    - service
- Variables, Loops and Conditionals

#### Tasks

- Really perform changes on systems
- Call different modules

##### Install a package

- Packages can be installed using the *package* module
    - https://docs.ansible.com/ansible/latest/modules/package_module.html#package-module

```
- name: "Install vim"
  package:
    name: "vim"
    state: "present"
```

- Avoid multiple blocks of same code, use loops *with_items*:

```
- name: "Install basic packages"
  package:
    name: "{{ item }}"
    state: "present"
  with_items:
    - vim
    - tmux
```

- Make list of packages parameterized
    - Only run task if variable is set with *when* conditionals

```
# inventory/preproduction/host_vars/www01
common__host_packages:
  - screen

# tasks/main.yml
- name: "Install host specific packages"
  package:
    name: "{{ item }}"
    state: "present"
  with_items: "{{ common__host_packages }}"
  when: common__host_packages is defined
```

#### Deploy public keys

- Public keys can be deployed using the *authorized_key* module
    - https://docs.ansible.com/ansible/latest/modules/authorized_key_module.html#authorized-key-module
    - Avoid multiple blocks, use multiline variables

```
# inventory/preproduction/group_vars/all.yml
common__authorized_keys: |
  ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIP6Xe46nYk6s6KPDmQUGYfQFPm9yVptwdsYdbnjQZzOO wreiner@pluto
  ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCtTDqOXTMCWlb7nUgcwUjHQzNV0TKt0J0XgpycoxYRwYyM7YgcYoB/oOJ65ypX0RRdfSsatpoBUINixAGEVmU/3YdARWOR8/Sr+UKFjQ7f4NvWVl0HZw/6m7h6BcqFthQ7U/YiLkNqu4fuPIIXVl2xtAAM//4xJx575gxVvEFQ0qenIGWi8Ax5hODFq1lvoZIQNqki9Tyr2QGK86+Y8Lx/tHGnYFqHDxnL/dPR6QF5J89uYolL9bsCraGyJEJwT8/ww522VZiiKrZ7BbKiaNBX6HjYyhqP4UPVrNbT6QxdhwYfuy3wv8KMdE5CH5EaEXDWWhkc85utTfp/KmsZYdEZ /home/wreiner/.ssh/id_rsa
  ssh-dss AAAAB3NzaC1kc3MAAACBAMHy9t1h+iqZF8otJA6966blZ2hqL+19SlD9vozTLguOf/1GnYQeRHiMqiC2dC7AZHwi7Y4i4o+rzVJ1m4HvvLmS24czu2d7RWQ6ccjrcq7Kcvyam59CkdbBHltayO90H1dldon5A9pLBiqTn6/SJJXQ8YyHsJ4DkJ3wf3AgYk+LAAAAFQCAbtbtGmmB6I+WyV9bCnqdH6k3LwAAAIBVk+dFRtzmv/q8B8wKu6dvOk6uCWUgj5KfobyHOXf4gHaDL14QewQzJy8boffuIR5qMOzFAqyxWYXUFvMb1mDTRylDzzOBhDZZPHhFmbj1cbUVWuwAoNhqKxpKTKORc7htFOp5uUOGUzAIWauSGGgXAocSEJfiONRPLJNYTqGKHwAAAIB6pRheLA0kc2W+xwpxtF6JIVF/FdKk1xR55g3bHQUvqkmQLMWvLTDSflt3RHdzDYJ/YlSL5O5FQY5AoB9X36E+BDsyxlTIAdk7lyxzR8Q368BnLE+RCt0pCzJpKT/cXoT/z3Ah6maYX1Vdv5sksimI0BEyqq91Nl+/x9dbNDdwNA== wreiner@wreinerws
  ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQD1wMxZ8wZ6cTnTMzCKhwhx1IPZOTLTkR+6TPyS56+c3eu/gNNaF4WqFyCZkuxdx7rzs5eWSPqApT/6Tua+GX/abHwpimtmh4uuWVZNekmTcFRK8sh4oJTHMUqdTiXeqatrw72qiWEXrFPc4IYoOMtE8e3ENoQ6sHzYgpnqV8fTfhL27FXFnqgaDw7H0Mg43TF3i/nKd4YcOYE8TJdyCIAvXyAUdfpFgMX2dPW4tok/ieU022kvwUgst3l3E+l8ar9otpg1+Ib2Va/JRLfDSUBb8de0szdAzTbKjoKcdps/w51zIfcZlmgq4ox/ZA54HDa0uUx7JU+/Te4CIq79KBRb wreiner@wreinerws
  ssh-dss AAAAB3NzaC1kc3MAAACBAObQ8O12fJVDCaVt0j11vopl/20706YP4lM1h8SqP3+tTtKKwsS22XWHZUSxowQhRqcH/jDExm3ZHnvsF333m6i6ET7DPvhMFJZxKDDQ/S6uYbCWw1YF8fKfdVfCQ0Sh+QgfIG+G23FS2q7eH71mnin2btd5nP9C84kgqH6oUi07AAAAFQDyHu3+GgbZNiBURIDQJJzfxJui4wAAAIEAvbzBRe1RXYZUc3RL5Pa8wV6o5+1EvsdhaatfD8dYTnr9wyWKBVoGUl98DNP4G/BBv4/GV18Y4HPS3/H5s43T7TdtEtmxkolJH8lqBXvQ13VP3yejU1MOv0CmaU4aZPLxGXEszRux6V20QE9SP8Y/6mdjep67NNfC3uq9DEVZ8+8AAACBAL647OEHW+yAtF/hhqgQKRkVMuLFe33DVA7VHo1yG8DYXep8BcWZQ4lc1OSXyKAcJceRtpXGKcsIAFJfkUKxGwAgt9YkpFV2TerCMyt6GreRI8JiPdoJSE4zsgm9SR9SfQPWCJ1PQixVQt2y60MS20FOS3w4KaJhCJB00c53Hkjf wreiner@wreinerws

# tasks/main.yml
- name: "Deploy public keys"
  authorized_key:
    user: "centos"
    state: "present"
    key: "{{ common__authorized_keys }}"
  when: common__authorized_keys is defined
```

#### Disallow agent forwarding

- Change line in a config file using the *lineinfile* module
    - Change line vs. deploy whole file
    - https://docs.ansible.com/ansible/latest/modules/lineinfile_module.html#lineinfile-module

```
- name: "Disallow agent forwarding"
  lineinfile:
    path: /etc/ssh/sshd_config
    regexp: '^#?AllowAgentForwarding'
    line: "AllowAgentForwarding no"
```

- Restart the service

```
- name: "Restart ssh daemon"
  service:
    name: "sshd"
    state: "restarted"
    enabled: "yes"
```

#### Restart sshd service when config is changed

- Register the state of a task run using *register*
    - Check the state with *debug*

```
- name: "Disallow agent forwarding"
  lineinfile:
    path: /etc/ssh/sshd_config
    regexp: '^#?AllowAgentForwarding'
    line: "AllowAgentForwarding no"
  register: sshd_config_changed

- debug:
    msg: "{{ sshd_config_changed }}"
```

- Restart the service if the file was modified

```
- name: "Restart ssh daemon"
  service:
    name: "sshd"
    state: "restarted"
  when: sshd_config_changed.changed
```
