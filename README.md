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

### Keystone (set by this role)

| Name | Default value | Description | Note |
|---  |---  |---  |--- |
| `admin_pass` | `admin_pass_default` | Desired admin password ||
| `admin_token` | `admin_token_default` | Desired service token ||
| `demo_pass` | `demo_pass_default` | Desired demo password ||
| `keystone_admin_port` | `35357` | Desired keystone admin service port ||
| `keystone_hostname` | `localhost` | Hostname/IP address where this role runs, it will be used to set keystone endpoints ||
| `keystone_port` | `5000` | Desired keystone service port ||
| `keystone_protocol` | `http` | Desired keystone protocol (http/https) | WiP, do not use. |


### MySQL (must exist)

| Name | Default value | Description | Note |
|---  |---  |---  |--- |
| `mysql_hostname` | `localhost` | MySQL server address ||
| `mysql_keystone_db` | `mysql_keystone_db` | Keystone db name ||
| `mysql_keystone_user` | `mysql_keystone_user` | keystone db user ||
| `mysql_keystone_pass` | `mysql_keystone_pass` | Keyston db password ||


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
          keystone_hostname: "{{ ansible_eth0.ipv4.address }}"

---

A complete Ansible playbook demo, which uses this role, is available on Github (dguerri/vagrant-ansible-openstack) <https://github.com/dguerri/vagrant-ansible-openstack>

---


License
-------

Apache

Author Information
------------------

Davide Guerri - davide.guerri@gmail.com
