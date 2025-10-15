# SQLite
Execute SQLite commands.

## Requirements
[supported platforms](https://github.com/r-pufky/ansible_sqlite/blob/main/meta/main.yml)

## Role Variables
[defaults](https://github.com/r-pufky/ansible_sqlite/tree/main/defaults/main/)

### Generated Variables
After successful execution the following variables are available for further
manipulation during the same play (standard role variable scope):

 Variable            | Type | Description
---------------------|------|-----------------------------------------
 _sqlite_sql_results | dict | registered return results from command.

## Dependencies
**galaxy-ng** roles cannot be used independently. Part of
[r_pufky.srv](https://github.com/r-pufky/ansible_collection_srv) collection.

## Example Playbook
Optionally installs, vacuums, then executes SQL commands against a SQLite
database.

Queries should be quoted for command line usage; try the `quote` filter.

### Execute a SQL query
roles/my_custom_role/tasks/task.yml
``` yaml
- name: 'Query database version'
  ansible.builtin.include_role:
    name: 'r_pufky.srv.sqlite'
  vars:
    sqlite_sql: 'select max(Version) from VersionInfo;'
    sqlite_db: '/tmp/test.db'

- name: 'Results'
  ansible.builtin.debug:
    msg: '{{ _sqlite_sql_results }}'
```

### Vacuum Database
``` yaml
- name: 'Clean database'
  ansible.builtin.include_role:
    name: 'r_pufky.srv.sqlite'
  vars:
    sqlite_db: '/tmp/test.db'
    sqlite_vacuum: true
```

### Install SQLite, execute SQL query as root user, and vacuum database
``` yaml
- name: 'Install, query, and vacuum database'
  ansible.builtin.include_role:
    name: 'r_pufky.srv.sqlite'
  vars:
    sqlite_sql: 'select max(Version) from VersionInfo;'
    sqlite_db: '/tmp/test.db'
    sqlite_vacuum: true
    sqlite_install: true
    sqlite_become: true
    sqlite_become_user: 'root'

- name: 'results'
  ansible.builtin.debug:
    msg: '{{ _sqlite_sql_results }}'
```

## Development
Configure [environment](https://github.com/r-pufky/ansible_collection_docs/blob/main/ansible/environment.md)

Run all unit tests:
``` bash
molecule test --all
```

### Releases
Release format: **{OS}-{SERVICE}-{ROLE}**

Each type inherits the versioning system used; defaulting to schematic
versioning.

`12.0.0-2.0.3-1.0.0`

* 12.0.0 - Debian 12 (bookworm).
* 2.0.3 - Service/app version.
* 1.0.0 - Role version.

Releases are branched on Debian releases:

* **[13.x.x](https://github.com/r-pufky/ansible_sqlite)**: 13 Trixie.
* **[12.x.x](https://github.com/r-pufky/ansible_sqlite/tree/12.x)**: 12 Bookworm.

### Issues
Create a bug and provide as much information as possible.

Associate pull requests with a submitted bug.

## License
[AGPL-3.0 License](https://www.tldrlegal.com/license/gnu-affero-general-public-license-v3-agpl-3-0)
 [(direct link)](https://github.com/r-pufky/ansible_sqlite/blob/main/LICENSE)

## Author Information
PGP Fingerprint: [466EEC2B67516C7117C85CE3A0BC35D16698BAB9](https://keys.openpgp.org/vks/v1/by-fingerprint/466EEC2B67516C7117C85CE3A0BC35D16698BAB9)
| [github gist](https://gist.github.com/r-pufky/a8df36977c55b5bb20829267c4c49d22)
