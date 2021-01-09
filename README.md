# Ansible Role: HashiCorp Boundary

A role to deploy [HashiCorp Boundary](https://www.boundaryproject.io/)

## Requirements

- A PostgreSQL instance that Boundary workers can reach and authenticate to. The database you plan to use must also exist.
- Access to a KMS solution. This role currently only supports Google Cloud KMS.
- Nodes must be in inventory groups `boundary_controller` or `boundary_worker` to receive configuration for that service.
  A node in both groups is configured to run both services.

## Installation Variables

### Package Installation

On RedHat and Debian family operating systems, it defaults to installing the packages from Hashicorp's official repository.
You can disable this by setting `boundary_install_package` to false.

### Manual Installation

*The following values are only used for manual installation.*

Controls whether a separate account is created or not and what the user and group should be named.

```YAML
boundary_user: 'boundary'
boundary_group: 'boundary'
boundary_create_account: true
```

Controls what is downloaded, and where it is installed.

```YAML
boundary_archive: 'boundary_{{ boundary_version }}_linux_amd64.zip'
boundary_download: 'https://releases.hashicorp.com/boundary/{{ boundary_version }}/{{ boundary_archive }}'
boundary_data_directory: '/opt/boundary'
boundary_install_directory: '{{ boundary_data_directory }}/bin'
```

## Configuration Variables

Ansible variables are listed below, along with the default values (see `default/main.yml`):

Where to place Boundary's configuration data.

```YAML
boundary_version: '0.1.4'
boundary_home_directory: '/etc/boundary.d'
boundary_config_file: '{{ boundary_home_directory }}/boundary-worker.hcl'
boundary_server_file: '{{ boundary_home_directory }}/boundary-controller.hcl'
```

### Database initialization flags

Boundary can create an example admin account and organization to help bootstrap you.
This is disabled by default since uses will create the initial resources via Ansible.
If you are building a PoC to learn and explore, you may want to remove this value.

```YAML
boundary_db_init_flags: '-skip-initial-login-role'
```

### Key Management

One of the Boundary KMS types from [https://www.boundaryproject.io/docs/configuration/kms]

As these choices are radically different depending on your KMS, refer to one of these examples:

-- [GCP CKMS](docs/kms_gcp.md)
-- [Hashicorp Vault - Transit secrets engine](docs/kms_transit.md)

## Dependencies

None.

## Example Project with Vault KMS

https://github.com/dockpack/vault\_dojo.git

## Example Playbook

If you are new to Ansible playbooks and group vars, the following examples can guide you:

- Creating [Boundary Playbook](docs/playbook.md)
- Creating [Boundary Group Vars](docs/group_vars.md)

## Author Information

Jacob Mammoliti
Bas Meijer
Jo Rhett
