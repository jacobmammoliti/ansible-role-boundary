Ansible Role: HashiCorp Boundary
=========

A role to deploy [HashiCorp Boundary](https://www.boundaryproject.io/)

Requirements
------------

A PostgreSQL instance that Boundary workers can reach and authenticate to.

Role Variables
--------------

Ansible variables are listed below, along with the default values (see `default/main.yml`):

Controls whether the host is a Boundary worker or controller type.

```YAML
boundary_node_type: 'worker'
```

Controls whether a separate account is created or not and what the user and group should be named.

```YAML
boudary_user: 'boundary'
boundary_group: 'boundary'
boundary_create_account: true
```

Where to initialize Boundary's home, data, and install directory.

```YAML
boundary_home_directory: '/etc/boundary.d'
boundary_data_directory: '/opt/boundary'
boundary_install_directory: '{{ boundary_data_directory }}/bin'
boundary_config_file: '{{ boundary_home_directory }}/boundary-worker.hcl'
boundary_server_file: '{{ boundary_home_directory }}/boundary-controller.hcl'
```

The version of boundary to install and where it should download its binary from.

```YAML
boundary_version: '1.8.4'
boundary_archive: 'boundary_{{ boundary_version }}_linux_amd64.zip'
boundary_download: 'https://releases.hashicorp.com/boundary/{{ boundary_version }}/{{ boundary_archive }}'
```

Dependencies
------------

None.

Example Playbook
----------------

```YAML
- hosts: all
  become: yes
  roles:
      - role: ansible-role-boundary
```

Author Information
------------------

Jacob Mammoliti