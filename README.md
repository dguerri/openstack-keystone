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
| `keystone_database_url` | `sqlite:////var/lib/keystone/keystone.db` | Database URI ||
| `keystone_hostname` | `localhost` | Hostname/IP address where this role runs, it will be used to set keystone endpoints ||
| `keystone_admin_port` | `35357` | Desired keystone admin service port ||
| `keystone_port` | `5000` | Desired keystone service port ||
| `keystone_protocol` | `http` | Desired keystone protocol (http/https) | WiP, do not use. |
| `keystone_admin_token` | `keystone_admin_token` | Desired service token ||
| `keystone_tenants` | [] | Array of of hash with tenant `name` and `description` (see examples) ||
| `keystone_users` | [] | Array of hash with user: `name`, `password`, `tenant` and `email` (see examples) ||
| `keystone_roles` | [] | Array of hash with role: `name`, `user` and `tenant` (see examples) ||
| `keystone_services` | [] | Array of hash with role: `name`, `service_type` and `description` (see examples) ||
| `keystone_endpoints` | [] | Array of hash with role: `service_name`, `region`, `public_url`, `internal_url` and `admin_url` (see examples) ||


Dependencies
------------

None.

Example Playbook
----------------

    - hosts: keystone001
      roles:
        - role: openstack-keystone
          keystone_database_url: "mysql://{{ MYSQL_KEYSTONE_USER }}:{{ MYSQL_KEYSTONE_PASS }}@{{ DATABASE_HOSTNAME }}/{{ MYSQL_KEYSTONE_DB }}"
          keystone_hostname: "{{ ansible_eth0.ipv4.address }}"
          keystone_admin_token: "{{ ADMIN_TOKEN }}"
          keystone_tenants:
            - { name: admin, description: "Admin tenant" }
            - { name: demo, description: "Demo tenant"  }
          keystone_users:
            - name: admin
              password: "{{ ADMIN_PASS }}"
              tenant: admin
              email: admin@localhost
            - name: demo
              password: "{{ DEMO_PASS }}"
              tenant: demo
              email: "demo@localhost"
          keystone_roles:
            - { name: admin, user: admin, tenant: admin }
            - { name: _member_, user: demo, tenant: demo  }
          keystone_services:
            - name: keystone
              service_type: identity
              description: Keystone identity service
              status: present
          keystone_endpoints:
            - service_name: keystone
              public_url: "http://{{ ansible_eth0.ipv4.address }}:5000/v2.0"
              internal_url: "http://{{ ansible_eth0.ipv4.address }}:5000/v2.0"
              admin_url: "http://{{ ansible_eth0.ipv4.address }}:35357/v2.0"
              status: present

---

A complete Ansible playbook demo, which uses this role, is available on Github (dguerri/vagrant-ansible-openstack) <https://github.com/dguerri/vagrant-ansible-openstack>

---


License
-------

Apache

Author Information
------------------

Davide Guerri - davide.guerri@gmail.com
