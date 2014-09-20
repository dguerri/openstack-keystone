Keystone
=========

OpenStack Keystone identity service installation

_Tested on Ubuntu Precise (12.04) and Trusty (14.04)_

Requirements
------------

A MySQL server. See `mysql_hostname`, `mysql_admin_username` and
`mysql_rootpass` below.


Role Variables
--------------

# Other systems/serivces
* `mysql_hostname`:       MySQL server address. Defaults to "localhost".
* `mysql_admin_username`: MySQL admin username. Defaults to "root".
* `mysql_rootpass`:       MySQL admin password. Defaults to "mysql\_root\_default".

# Role specific
* `keystone_hostname`:    hostname/IP address where this role runs.
                          It will be used to set keystone endpoints.
                          Defaults to the first interface IP address (i.e., eth0).

* `keystone_dbpass`:      Desired keystone user password for the keystone database.
                          Defaults to "keystone\_dbpass\_default".

* `admin_token`:          Desired service token. Defaults to "admin\_token\_default".
* `admin_pass`:           Desired admin password. Defaults to "admin\_pass\_default".
* `demo_pass`:            Desired demo password. Defaults to "demo\_pass\_default".

* `keystone_admin_port`:  Desired keystone admin service port. Defaults to "35357".
* `keystone_port`:        Desired keystone service port. Defaults to "5000".

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: keystone001
      roles:
        - role: openstack-keystone
          mysql_rootpass: "{{ MYSQL_ROOT }}"
          keystone_dbpass: "{{ KEYSTONEDB_PASS }}"
          admin_token: "{{ ADMIN_TOKEN }}"
          admin_pass: "{{ ADMIN_PASS }}"
          demo_pass: "{{ DEMO_PASS }}"

License
-------

Apache

Author Information
------------------

Davide Guerri - davide.guerri@gmail.com
