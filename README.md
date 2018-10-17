postgresql
==========

This role installs and configures [PostgreSQL](https://postgresql.org/) into your system.

Requirements
------------

No special requirements; note that this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role in your playbook like:

    - hosts: database
      roles:
        - role: geerlingguy.postgresql
          become: yes

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

 * Packages to install for each OS: `postgresql_package`

```yaml
---
postgresql_package:
  RedHat: postgresql-server
  Debian: postgresql
```

 * PostgreSQL cluster initialization command (this is only used for RedHat based distributions):

```yaml
---
postgresql_cluster_init:
  v6: "service postgresql initdb"
  v7: "postgresql-setup initdb"
```

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in
regards to parameters that may need to be set for other roles, or variables that
are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables
passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: postgresql, x: 42 }

License
-------

Apache 2.0

Author Information
------------------

[Bithium S.A.](https://www.bithium.com/)
