openldap_server
===============

This roles installs the OpenLDAP server on the target machine. It has the
option to enable/disable SSL by setting it in defaults or overriding it.

Requirements
------------

This role requires Ansible 2.5 or higher, and platform requirements are listed
in the metadata file.

Role Variables
--------------

The variables that can be passed to this role and a brief description about
them are as follows:

    openldap_serverdomain_name: example    # The domain prefix for ldap
    openldap_server_domain_tld: com        # the tld for the domain
    openldap_server_rootpw: passme              # This is the password for admin for openldap
    openldap_server_enable_ssl: true            # To enable/disable ssl for the ldap
    openldap_server_country: US                 # The self signed ssl certificate parameters
    openldap_server_state: Oregon
    openldap_server_location: Portland
    openldap_server_organization: IT

The initial user and group mappings in the following format:
```
users:
  - admin
  - user1
  - user2

ldap_groups:
  - name: allUsers
    members:
      - admin
      - user1
      - user2
  - name: admins
    members:
      - admin
```

Examples
--------

1) Configure an OpenLDAP server without SSL:
```
---
- hosts: all
  sudo: true
  roles:
  - role: bennojoy.openldap_server
    openldap_server_domain_name: example
    openldap_server_domain_tld: com
    openldap_server_rootpw: passme
    openldap_server_enable_ssl: false
```
2) Configure an OpenLDAP server with SSL:
```
---
- hosts: all
  sudo: true
  roles:
  - role: bennojoy.openldap_server
    openldap_server_domain_name: example
    openldap_server_domain_tld: com
    openldap_server_rootpw: passme
    openldap_server_enable_ssl: true
    openldap_server_country: US
    openldap_server_state: Oregon
    openldap_server_location: Portland
    openldap_server_organization: IT
```

Dependencies
------------
- Need python-ldap on all the host machines.
- Suse also needs python-xml for ansible to run.
- Debian 9 needs python2 for ansible to run

None

License
-------

BSD

Author Information
------------------

Benno Joy

Endre Zoltan Kovacs - added Suse support, and various fixes

