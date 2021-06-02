Ansible Role pgAgent
=========

[![CI Pipeline](https://github.com/jegj/ansible-role-pgagent/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/jegj/ansible-role-pgagent/actions/workflows/ci.yml)

Install [pgAgent](https://www.pgadmin.org/docs/pgadmin4/development/pgagent.html) package, create the postgres extension and start pgAgent as a systemd unit for a target Postgresql database server on Debian/Ubuntu.

Requirements
------------

None

Role Variables
--------------

    pgagent_database: ""

Target database for pgAGent. **REQUIRED**, Otherwise the role will fail

    pgagent_database_port: 5432

Target postgres database port. Default to `5432`

    pgagent_upgrade: false

Allow to upgrade `pgagent` apt package if required. Default to `false`

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
    - jegj.pgagent
```

License
-------

BSD

Author Information
------------------

[Javier Galarza](https://jegj.github.io/resume/)
