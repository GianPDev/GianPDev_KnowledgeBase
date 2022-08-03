---
tags: [bash, linux, server, shell, fish, visudo]
---

### Ansible Location
```bash
sudo vi /etc/ansible/hosts
```

### More readable output when using -v (verbose)
```bash
sudo vi /etc/ansible/ansible.cfg
```
add (this should *beautify* the json):
```bash
[defaults]
stdout_callback = unixy
```

### Ping group
```bash
ansible GROUP -m ping
```

### Run command on group
```bash
ansible GROUP -a "cat /etc/os-release"
```
```bash
ansible GROUP -a "hostnamectl"
```

### Running Ansible Playbook with selected hosts
```yaml
---
- name: Update CentOS systems
  hosts: {{ select_hosts }}
  become: yes
  tasks:
   - name: update cache
     yum: update_cache=yes
   - name: update packages
     yum: name=* state=latest
```
Then run:
```bash
ansible-playbook --extra-vars "select_hosts=centos" centos-update.yaml
```