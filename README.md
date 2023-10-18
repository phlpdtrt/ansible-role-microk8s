[![CI](https://github.com/phlpdtrt/ansible-role-microk8s/actions/workflows/ci.yml/badge.svg)](https://github.com/phlpdtrt/ansible-role-microk8s/actions/workflows/ci.yml)
![MIT](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)
![GitHub last commit](https://img.shields.io/github/last-commit/phlpdtrt/ansible-role-microk8s?style=flat-square)
![GitHub Release Date](https://img.shields.io/github/release-date/phlpdtrt/ansible-role-microk8s?style=flat-square)

# Ansible Role: microk8s

Install and configure [microk8s](https://microk8s.io/) - the smallest, simplest, pure production K8s on debian based systems.

## Requirements

* Ansible >= 2.10
* Linux Distribution
    * Debian Family
      * Ubuntu
        * Focal (20.04)
        * Jammy (22.04)
      * Debian
        * Bullseye (11)
        * Bookworm (12)

## Usage

### Role Variables

Some variables available in this role are listed here.  The full set is
defined in `[defaults/main.yml](defaults/main.yml)`.
* `microk8s_plugins`: Enable/disable various plugins.
* `microk8s_enable_ha`: Enable/disable high-availability.
* `microk8s_group_ha`: Hostgroup whose members will form HA cluster.
* `microk8s_csr_template`: If defined, will cause a custom CSR to be used in
  generating certificates.

### Basic playbook

```yaml
- hosts: servers
  roles:
    - role: phlpdtrt.microk8s
      vars:
        microk8s_plugins:
          istio: true
          ingress: true
```

### High Availability clusters

Setting up a High Availability cluster is very simple with MicroK8s.

* Set `microk8s_enable_ha` to `true`
* Set one of the nodes as the master node (The nodes all others will join to)

Example inventory:
```ini
[infra_master]
gp-central-awx0 ansible_host=a.b.c.d ansible_user=ansible is_master=true
```

### Character encoding

On some system the default character set is ASCII which breaks MicroK8s a bit. The solution to this is to set the
encoding to UTF-8: `export LC_ALL=C.UTF-8`

## License

MIT
