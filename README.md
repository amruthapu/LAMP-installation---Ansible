# LAMP installation - Ansible

LAMP is an acronym denoting one of the most common software stacks for many of the web's most popular applications. However, LAMP now refers to a generic software stack model and its components are largely interchangeable. Here, I'm installing LAMP software in a Linux server using ansible playbook. 

## Tasks

- Install LAMP ( Apache, MySQL, PHP ) 

## Install LAMP

Here, I'm installing LAMP at the remote server using playbook.

```bash
---
- name: Install LAMP in the remote servers
  hosts: all
  tasks:
    - name: Install LAMP
      yum:
        name: "{{ item }}"
        state: latest
      with_items:
      - httpd
      - mariadb-server
      - php
    - name: Start services
      service:
         name: "{{ item }}"
         state: started
         enabled: true
      with_items:
      - httpd
      - mariadb
```

## Output

```bash

PLAY [Install LAMP in the remote servers] ***********************************************************************************************
 
TASK [Gathering Facts] ******************************************************************************************************************
ok: [44.201.236.231]
 
TASK [Install LAMP] *********************************************************************************************************************
ok: [3.91.227.46] => (item=[u'httpd', u'mariadb-server', u'php'])
ok: [44.201.236.231] => (item=[u'httpd', u'mariadb-server', u'php'])
changed: [54.209.196.143] => (item=[u'httpd', u'mariadb-server', u'php'])
 
TASK [Start services] *******************************************************************************************************************
ok: [3.91.227.46] => (item=httpd)
ok: [44.201.236.231] => (item=httpd)
ok: [3.91.227.46] => (item=mariadb)
ok: [44.201.236.231] => (item=mariadb)
changed: [54.209.196.143] => (item=httpd)
changed: [54.209.196.143] => (item=mariadb)
 
PLAY RECAP ******************************************************************************************************************************
3.91.227.46                : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
44.201.236.231             : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
54.209.196.143             : ok=3    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```
