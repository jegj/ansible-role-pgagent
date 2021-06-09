Ansible Role pgAgent
=========

[![CI Pipeline](https://github.com/jegj/ansible-role-pgagent/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/jegj/ansible-role-pgagent/actions/workflows/ci.yml)


1) Install [pgAgent](https://www.pgadmin.org/docs/pgadmin4/development/pgagent.html) package.
2) Install( or Upgrade ) the pgAgent extension on the target database( if the database is local ).
3) Create a configuration file for the target database.
4) Start a pgAgent systemd unit for a target database.

On a Debian/Ubuntu system.

Requirements
------------

None

Role Variables
--------------

    pgagent_database: ""

Target database for pgAGent. **REQUIRED**, Otherwise the role will fail.

    pgagent_database_port: 5432

Target database port for pgAgent. Default to `5432`.

    pgagent_upgrade: false

Allow to upgrade `pgagent` apt package if required. Default to `false`.

    pgagent_user: "postgres"

Target user for pgAgent. Default to `postgres`.

    pgagent_hostaddr: "my.testdb"

Database Host address for pgAgent. **NO DEFINED**. By default the role use a local connection to the database.

    pgagent_password: "myp4$$word"

User's password for pgAgent connection if is required. **NO DEFINED**. By default use postgres user with peer authentication.

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
pgAgent Unit Configuration File
----------------
The role will create a configuration file per database located at `/etc/pgagent/{{ your_db }}.conf` with the following configuration options:

- `PG_AGENT_TARGET_PORT`: Postgres Database port.
- `PG_AGENT_HOST_ADDR`: Postgres Database host. If the connection is local this variable is not present.
- `PG_AGENT_USER`: Postgres Database user. Default to `postgres`.
- `PG_AGENT_LOG_VERBOSITY`: pgAgent Verbosity. Default to `1`(WARNING). Allowed values: (ERROR=0, WARNING=1, DEBUG=2).
- `PG_AGENT_RETRY_PERIOD`: pgAgent retry period after connection abort in seconds. Default to `30`.
- `PG_AGENT_POLL_INTERVAL`: pgAgent poll time interval in seconds. Default to `10`.

Restart the pgagent unit for the target database to use the new configuration options with the following command:
```sh
sudo systemctl restart pgagent@{{ your_db }}
```

Check [here](https://www.pgadmin.org/docs/pgadmin4/development/pgagent_install.html#daemon-installation-on-unix) for more information

To show stats about your pgAgent unit run:
```sh
sudo systemctl status pgagent@{{ your_db }}
```
pgAgent Log File
----------------
The pgAgent systemd unit will log to the file `/var/log/pgagent/{{ your_db }}.log` by default. There is also an entry at `/etc/logrotate.d/pgagent` that will rotate the log weekly by default.

License
-------

BSD

Author Information
------------------

[Javier Galarza](https://jegj.github.io/resume/)
