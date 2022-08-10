# Role Name
![CI Testing](https://github.com/linux-system-roles/template/workflows/tox/badge.svg)

A template for an ansible role which configures some GNU/Linux subsystem or
service. A brief description of the role goes here.

## Requirements

Any pre-requisites that may not be covered by Ansible itself or the role should
be mentioned here. For instance, if the role uses the EC2 module, it may be a
good idea to mention in this section that the `boto` package is required.

## Role Variables

A description of all input variables (i.e. variables that are defined in
`defaults/main.yml`) for the role should go here as these form an API of the
role.

Example of setting the variables:

```yaml
postgresql_version: "13"
postgresql_password: "mysecretpassword"
```
## Optional Variables
A description of input variables that are not reqiured. Upstream configuration is used by default.
Usage of `pg_hba_conf` causes replacement of default upstream configuration
```yaml
pg_hba_conf:
  - { type: local, database: all, user: all, auth_method: peer }
  - { type: host, database: all, user: all, address: '127.0.0.1/32' auth_method: ident }
  - { type: host, database: all, user: all, address: '::1/128', auth_method: ident }
```
Usage of `postgresql_server_conf` adds defined values at the end of postgresql.conf.
So the default ones are overwritten.
```yaml
postgresql_server_conf:
  ssl: on
  shared_buffers: 128 MB
  huge_pages: try
```
To set up ssl connection it's necessary to set up `ssl_enable` variable and provide server certificate and key.
```
ssl_enable: on
```
To specify certificate name use `cert_name` variable. by default is set to:
```
cert_name: "server"
```
You can copy your certificate to `/etc/pki/tls/certs/server.crt` and key to `/etc/pki/tls/private/server.key` or
you can also use certificate system role. For more detail see examples.
## Dependencies

A list of other roles hosted on Galaxy should go here, plus any details in
regards to parameters that may need to be set for other roles, or variables
that are used from other roles.

## Example Playbook

Including an example of how to use your role (for instance, with variables
passed in as parameters) is always nice for users too:

```yaml
- hosts: all
  vars:
    postgresql_version: "13"
    postgresql_password: "passwd"

  roles:
    - postgresql-system_role
```

13More examples can be provided in the [`examples/`](examples) directory. These
can be useful especially for documentation.

## License

Whenever possible, please prefer MIT.

## Author Information

An optional section for the role authors to include contact information, or a
website (HTML is not allowed).
