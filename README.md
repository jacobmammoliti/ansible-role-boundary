Ansible Role: HashiCorp Boundary
=========

A role to deploy [HashiCorp Boundary](https://www.boundaryproject.io/)

Requirements
------------

- A PostgreSQL instance that Boundary workers can reach and authenticate to. The database you plan to use must also exist.
- Access to a KMS solution. This role currently only supports Google Cloud KMS.
- Nodes must be in inventory groups `boundary_controller` or `boundary_worker` to receive configuration for that service. 
  A node in both groups is configured to run both services.

Role Variables
--------------

Ansible variables are listed below, along with the default values (see `default/main.yml`):

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
boundary_version: '0.1.0'
boundary_archive: 'boundary_{{ boundary_version }}_linux_amd64.zip'
boundary_download: 'https://releases.hashicorp.com/boundary/{{ boundary_version }}/{{ boundary_archive }}'
```

The type of KMS to use.

```YAML
boundary_kms_type: 'gcpckms'
```
Or
```
boundary_kms_type: 'transit'
```

Dependencies
------------

None.

Example Project with Vault KMS
------------------------------
https://github.com/dockpack/vault\_dojo.git


Example Playbook
----------------
The following deploys a single Boundary controller and worker node.

Create an inventory file:
```bash
$ cat > inventory <<EOF
[boundary_controllers]
192.168.0.100

[boundary_workers]
192.168.0.101
EOF
```

Create the group_vars directory and file:
```bash
# ensure the group_vars directory exists
$ mkdir group_vars/

# create the group_vars file for all hosts
$ cat > group_vars/all.yml <<EOF
---
boundary_psql_endpoint: ''
boundary_psql_username: ''

boundary_gcpckms_project: ''
boundary_gcpckms_region: ''
boundary_gcpckms_keyring: ''
boundary_gcpckms_key: ''
EOF
```

Run the playbook (Boundary PSQL password should be passed through a more secure method so it isn't shown in plaintext):
```bash
$ ansible-playbook -i inventory site.yml --extra-vars "boundary_psql_password=''"
```

Author Information
------------------

Jacob Mammoliti
Bas Meijer
