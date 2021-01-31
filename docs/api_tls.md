# Boundary Controller API TLS example

## Acquire a certificate the client OS will trust

This could be from any source the host OS will trust:

- an internal CA trusted by all clients
- LetsEncrypt
- ...any other signing authority trusted by the OS

## Configure Boundary to use the TLS Certificate

You must explicitly enable TLS:

```YAML
boundary_tls_disable: false
```

You can override the default locations where the key and certifcate is installed

```YAML
# default locations for API TLS keys and certificates
boundary_api_tls_path:      "{{ boundary_home_directory }}/tls" # create directory if defined
boundary_api_tls_cert_file: "{{ boundary_api_tls_path }}/api_cert.pem"
boundary_api_tls_key_file:  "{{ boundary_api_tls_path }}/api_key.pem"
```

### Ansible secrets

Best practice would be to supply the key and certificate from a secret store, such as Ansible Vault:

```YAML
boundary_api_tls_cert_content: secret_variable_name
boundary_api_tls_key_content: secret_variable_name
```

### Copy from files on disk (local or remote)

If the files are available on disk, you can simply copy the files into place.

```YAML
boundary_api_tls_src_path: 'files/tls' # only used within other values, relative to the playbook when local
boundary_api_tls_cert_src_file: "{{ boundary_api_tls_src_path }}/client_cert.pem"
boundary_api_tls_cert_src_remote: false
boundary_api_tls_key_src_file: "{{ boundary_api_tls_src_path }}/client_key.pem"
boundary_api_tls_key_src_remote: false
```

### Client validation

If you use an internal CA and do client validation, you must declare the CA used to validate:

```YAML
boundary_api_tls_ca_file:   "{{ boundary_api_tls_path }}/api_ca.pem"
boundary_api_tls_ca_src_file: "{{ boundary_api_tls_src_path }}/ca_cert.pem"
boundary_api_tls_ca_src_remote: false  # true to use remote file
#boundary_api_tls_ca_content: variable_name
```

*If you are supplying a public TLS certificate to avoid client errors, you don't need to supply the CA file.*
