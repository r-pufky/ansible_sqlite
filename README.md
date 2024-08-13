# SQLite
Execute SQLite commands.

## Requirements
[supported platforms](https://github.com/r-pufky/ansible_sqlite/blob/main/meta/main.yml)

[collections/roles](https://github.com/r-pufky/ansible_sqlite/blob/main/meta/requirements.yml)

## Role Variables
[defaults](https://github.com/r-pufky/ansible_sqlite/tree/main/defaults/main/)

### Generated Variables
After successful execution the following variables are available for further
manipulation during the same play (standard role variable scope):

 Variable        | type | Description
-----------------|------|-----------------------------------------
 _sqlite_results | dict | registered return results from command.

## Dependencies
N/A

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
    msg: '{{ _sqlite_results }}'
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

### Install SQLite, execute SQL query, and vacuum database
``` yaml
- name: 'Install, query, and vacuum database'
  ansible.builtin.include_role:
    name: 'r_pufky.srv.sqlite'
  vars:
    sqlite_sql: 'select max(Version) from VersionInfo;'
    sqlite_db: '/tmp/test.db'
    sqlite_vacuum: true
    sqlite_install: true

- name: 'results'
  ansible.builtin.debug:
    msg: '{{ _sqlite_results }}'
```

## Unit Testing
Test framework requires molecule and rootless podman setup.

Run all unit tests:
``` bash
molecule test --all
```

## Issues
Create a bug and provide as much information as possible.

Associate pull requests with a submitted bug.

## License
[AGPL-3.0 License](https://www.tldrlegal.com/license/gnu-affero-general-public-license-v3-agpl-3-0)
 [(direct link)](https://github.com/r-pufky/ansible_fonts/blob/main/LICENSE)

## Author Information
PGP Fingerprint: [466EEC2B67516C7117C85CE3A0BC35D16698BAB9](https://keys.openpgp.org/vks/v1/by-fingerprint/466EEC2B67516C7117C85CE3A0BC35D16698BAB9)
| [github gist](https://gist.github.com/r-pufky/a8df36977c55b5bb20829267c4c49d22)
