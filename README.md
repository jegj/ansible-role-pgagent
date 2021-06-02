Ansible Role pgAgent
=========

Install [pgAgent](https://www.pgadmin.org/docs/pgadmin4/development/pgagent.html) package, create the postgres extension and start pgAgent as a systemd unit for a target Postgresql database server on Debian/Ubuntu.

Requirements
------------

None

Role Variables
--------------

    pgAgent_database: ""

Target database for pgAGent. **REQUIRED**, Otherwise the role will fail

    pgAgent_database_port: 5432

Target postgres database port. Default to `5432`

    pgAgent_upgrade: false

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
