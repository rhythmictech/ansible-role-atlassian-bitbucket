# Ansible Role: Atlassian Bitbucket
![Molecule Test](https://github.com/rhythmictech/ansible-role-atlassian-bitbucket/workflows/Molecule%20Test/badge.svg)

Installs Atlassian Bitbucket, optionally automatically completing the auto-setup process.

The role can automatically install the MySQL JDBC driver if desired. MySQL is deprecated in modern versions of MySQL and requires certain MySQL settings to be in place for Bitbucket to work correctly.

## Requirements
This role requires Ansible 2.6 or higher.
This role was designed for and tested on CentOS 7.x or CentOS 8.x and Amazon Linux 2.

## Dependencies
None. This role will install OpenJDK 11 automatically from system package. Please note that this can conflict if the base image automatically installs a different JDK outside of the role.

## Example Playbook
```
- hosts: bitbucket_server
  vars_files:
    - vars/main.yml
  roles:
    - ansible-role-atlassian-bitbucket
```

Inside vars/main.yml:
```
bitbucket_start_service: True
bitbucket_enable_service: True
bitbucket_wait_for_server_startup: True
bitbucket_place_config: True
bitbucket_config:
	jdbc:
		driver: org.h2.Driver
		url: jdbc:h2:${bitbucket.shared.home}/data/db;MVCC=TRUE;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE;TRACE_LEVEL_FILE=4
		username: sa
		password: password
	server:
		address: 127.0.0.1

```

## License
MIT
