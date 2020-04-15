# tranquilit.waptserver

## Requirements

* Debian Linux or CentOS Virtual Machine
* Ansible 2.8 

## Install WAPT on a remote server

* git clone and install that role in `/etc/ansible/roles`

```
cd /etc/ansible/roles/
git clone https://github.com/tranquilit/ansible.waptserver
```

* ensure you have a working ssh key deployed as root on your WAPT server, if not you can generate and copy one like so :

```
ssh-keygen -t ed25519
ssh-copy-id -i id_ed25519.pub root@srvwapt.mydomain.lan
```

* add you WAPT server to Ansible hosts file

```
[srvwapt]
srvwapt.mydomain.lan ansible_host=192.168.1.40
```

* create a playbook with the following content in `/etc/ansible/playbooks/wapt.yml` :

```
- hosts: srvwapt
  roles:
    - { role: tranquilit.waptserver }
```

* run your playbook with the following command :

```
cd /etc/ansible/
ansible-playbook -i hosts playbooks/wapt.yml
```

That's it WAPT is installed on your server !

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

### WAPT server vars

WAPT version that will be installed from WAPT Deb/RPM repository

    wapt_version: "1.8"

PostgreSQL version that will be installed from WAPT Deb/RPM repository

    pgsql_version: "9.6"

CentOS version used for RPM repository address

    centos_version: "centos7"

`launch_postconf` defaults to True, it launches WAPT Server postconfiguration script silently

    launch_postconf: True

## Dependencies

None.

## Example Playbook

    - hosts: hosts
      vars_files:
        - vars/main.yml
      roles:
        - tranquilit.waptserver
