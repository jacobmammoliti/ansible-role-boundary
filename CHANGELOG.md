# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [v1.0.1]

### Fixed

- RedHat installation

## [v1.0.0]

### Breaking Changes

- Boundary cluster TLS is always enabled.
- `boundary_tls_disable` now controls Boundary Controller API TLS
- Configuration variables for Vault transit TLS have changed names.
  *This was required to allow secret-provided key/cert provisioning*

### Added

- Boundary API controller TLS config
- AEAD and AWS KMS types
- Documentation examples for each KMS Type

### Changes

- Boundary config file default paths
- Boundary default KMS `aead` to match Boundary dev deployment
- Start controller before worker

### Removed

- `boundary_tls_*` configuration options

## [v0.2.3]

### Added

- New variables to control Apt and Yum repo locations. Default to Hashicorp, can be overridden now
  - boundary_apt_repo
  - boundary_yum_repo
- YAML lint configuration

## [v0.2.2]

### Fixed

- Fix the flag passed to the database creation, which was wrong in source docs

## [v0.2.1]

### Changes

- Rename boundary_config task to config
- Reverse order of controller and worker config to avoid startup failures
- Fix template to reference unique group name changed earlier

## [v0.2.0]

### Changes

- Boundary version default to 0.1.4
- README markdown format changes
- Added ChangeLog
- Added version file

## Prior to version history

All changes since fork from [arctiqjacob/ansible-role-boundary](https://github.com/arctiqjacob/ansible-role-boundary)

### Added

- Install from package on Debian, RHEL, and macOS
- Ansible 2.10 support
- bash command completion
- ufw firewall support

### Changed

- database_init is now idempotent and configurable
- controller and worker group names have `boundary_` prefix
