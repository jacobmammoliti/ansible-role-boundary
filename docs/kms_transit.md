# Boundary Vault Transit KMS configuration

Based on [https://www.boundaryproject.io/docs/configuration/kms/transit]

## Requirements

* Hashicorp Vault implementation with Transit secret engine
* `VAULT_TOKEN` environment variable for a session with permissions described at
  [https://www.boundaryproject.io/docs/configuration/kms/transit#authentication]

## Configuration Steps

Create a group_vars file for boundary controller nodes

### `group_vars/boundary_controllers.yml`

Add the Vault transit keystore details

```YAML
# Required settings
boundary_kms_type: 'transit'
vault_instances:
  - vault.example.com
```

Then compare the key name, mount path, and namespace for the transit store
with the values in [../templates/boundary-controller.hcl.j2]

*Will be improved in a coming release*
