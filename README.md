Ansible Role pgAgent
=========

Install [pgAgent](https://www.pgadmin.org/docs/pgadmin4/development/pgagent.html) as a systemd unit for a Postgresql database server on Debian/Ubuntu

Requirements
------------

None

Role Variables
--------------

TODO:

Dependencies
------------

None

Example Playbook
----------------

```yaml
- hosts: dbserver
  vars_files:
    - vars/main.yml
  roles:
    - jegj.pgAgent
```

License
-------

BSD

Author Information
------------------

[Javier Galarza](https://jegj.github.io/resume/)
