# tranquilit.waptserver

## Requirements

* Debian Linux or CentOS Virtual Machine
* Ansible 2.9

## Install WAPT on a remote server

* git clone
Clone the repository in a working directory

```
cd /working/dir/
git clone https://github.com/tranquilit/ansible.waptserver
```

* ensure you have a working ssh key deployed as root on your WAPT server, if not you can generate and copy one like so :

```
ssh-keygen -t ed25519
ssh-copy-id -i id_ed25519.pub root@srvwapt.mydomain.lan
```
Go to production/inventory and/or staging/inventory and add your private key in
ansible_ssh_private_key_file



* Run your playbook with the following commands :

```
ansible-playbook site.yml -i staging

ansible-playbook site.yml -i production
```
You can deactivate the postconf launch with

```
ansible-playbook site.yml -i staging  -e "launch_postconf='false'"

ansible-playbook site.yml -i production  -e "launch_postconf='false'"

```

That's it WAPT is installed on your server !

## Role Variables

Available variables are listed below, along with default values (see `roles/waptserver/defaults/main.yml`):

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
