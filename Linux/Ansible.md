---
tags: [bash, linux, server, shell, fish, visudo]
---

*Note: My ansible installation is connected via ssh keys, thus not needing passwords to be entered at any point, also all of my servers are RHEL based (Centos/RockyLinux/AlmaLinux) all these notes are under this assumption.*

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

### Useful Ansible Collections
```bash
ansible-galaxy collection install ansible.posix
```
```bash
ansible-galaxy collection install community.general
```

### Ping group (good way to check if server is online and can be connected to)
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
ansible-playbook --extra-vars "select_hosts=GROUP" centos-update.yaml
```

### Fixing `Failed to detect selinux python bindings at ['/usr/local/lib64/python3.8/site-packages', ...` after installing python3.8 via ansible
If there's Centos 7 servers, python3.8 isn't available, try python36 (python3.6) instead.
try (around 350MB~ installed):
```bash
sudo yum install python3-libselinux setools 
```

add
```bash
-e 'ansible_python_interpreter=/usr/bin/python3'
```
to ansible/ansible-playbook line, try different python versions if one doesn't work (python3, python)
```bash
ansible GROUP -m ping -e 'ansible_python_interpreter=/usr/bin/python3'
```
If the above doesn't work, try install these too
```bash
sudo yum python3-setools setools-console setools-console-analyses
```

### Possible permanent fix so you don't need to type the above line every time
This may also help with some other issues; symlink-ing python3 to python on each affected server
```bash
ln -s /usr/bin/python3 /usr/bin/python
```

Note for the above two *solutions* I ran this [playbook](https://github.com/GianPDev/Ansible-Playbooks/blob/master/selinux-enable.yaml) that may have affected whether it worked (it tried to install python 3.8, python3 and pip installed selinux), but I believe the selinux problem should be solved by the two packages

### Error installing kernel needs 6MB on /boot filesystem
Error:
```
Transaction check error:
  installing package kernel-3.10.0-1160.76.1.el7.x86_64 needs 6MB on the /boot filesystem

Error Summary
-------------
Disk Requirements:
  At least 6MB more space needed on the /boot filesystem.
```
`sudo` was not installed, login to root and
```
yum install sudo
```
clean up /boot (this cleans all but last 2 kernels on the system)
```bash
sudo yum install yum-utils
```
```bash
sudo package-cleanup --oldkernels --count=2
```
```
sudo yum update kernel
```