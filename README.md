postgresql
==========

This role installs and configures [PostgreSQL](https://postgresql.org/) into your system.

Requirements
------------

No special requirements; note that this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role in your playbook like:

    - hosts: database
      roles:
        - role: bithium.postgresql
          become: yes

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml` and `vars/main.yml`):

 * Packages to install for each OS: `postgresql_package`

```yaml
---
postgresql_package_names:
  Debian: postgresql
  RedHat: postgresql-server

postgresql_package: "{{postgresql_package_names[ansible_os_family]}}"

postgresql_packages:
  - "{{postgresql_package}}"
```

 * PostgreSQL cluster initialization command (this is only used for RedHat based distributions):

```yaml
---
postgresql_cluster_init:
  RedHat: {
    v6: "service postgresql initdb",
    v7: "postgresql-setup initdb",
  }
```

 * Service name:

        postgresql_service: postgresql

 * Cluster name:

```yaml
---
postgresql_cluster_names:
  Debian: "{{postgresql_version}}/main"
  RedHat: "data"

postgresql_cluster_name: "{{postgresql_cluster_names[ansible_os_family]}}"
```

 * Cluster data folder:

```yaml
---
postgresql_var_lib_names:
  Debian: "postgresql"
  RedHat: "pgsql"

postgresql_var_lib_name: "{{postgresql_var_lib_names[ansible_os_family]}}"

postgresql_data_dir: "/var/lib/{{postgresql_var_lib_name}}/{{postgresql_cluster_name}}"
```

 * Cluster configuration folder:

```yaml
---
postgresql_config_dirs:
  Debian: "/etc/postgresql/{{ postgresql_cluster_name }}"

postgresql_config_dir: "{{postgresql_config_dirs[ansible_os_family] | default(postgresql_data_dir)}}"
```

 * Cluster configuration file:

        postgresql_config_file: "{{postgresql_config_dir}}/postgresql.conf"

 * Cluster custom configuration folder:

        postgresql_extra_config_dir: "{{postgresql_config_dir}}/conf.d"

 * Cluster custom configuration file:

        postgresql_extra_config_file: "{{postgresql_extra_config_dir}}/25_ansible.conf"

 * Cluster custom configuration options:

   This is an hash with the options that will be placed in `postgresql_extra_config_file` as `key = value`, e.g:

        postgresql_config:
           port: 4242
           max_connections: 50

Dependencies
------------

Example Playbook
----------------

    - hosts: servers
      become: true
      roles:
         - role: postgresql

License
-------

Apache 2.0

Author Information
------------------

[Bithium S.A.](https://www.bithium.com/)
