[![CI](https://github.com/de-it-krachten/ansible-role-syft/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-syft/actions?query=workflow%3ACI)


# ansible-role-syft

Installs syft, CLI tool and library for generating a Software Bill of Materials from container images and filesystems<br>
https://github.com/anchore/syft<br>



## Dependencies

#### Roles
None

#### Collections
- community.general
- ansible.posix

## Platforms

Supported platforms

- Red Hat Enterprise Linux 7<sup>1</sup>
- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- CentOS 7
- RockyLinux 8
- RockyLinux 9
- OracleLinux 8
- OracleLinux 9
- AlmaLinux 8
- AlmaLinux 9
- Debian 10 (Buster)
- Debian 11 (Bullseye)
- Ubuntu 18.04 LTS
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Fedora 35
- Fedora 36

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# Github CLI - API
syft_api: https://api.github.com/repos/anchore/syft

# Github CLI - repo
syft_repo: https://github.com/anchore/syft

# Lookup table for architecture
syft:
  architecture:
    x86_64: amd64
  system:
    Linux: linux
    Darwin: darwin

# Version of the CLI to install
syft_version: latest

# Location/ownership/permissions of the binary
syft_path: /usr/local/bin/syft
syft_owner: root
syft_group: root
syft_mode: '0755'
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'syft'
  hosts: all
  become: "yes"
  tasks:
    - name: Include role 'syft'
      ansible.builtin.include_role:
        name: syft
</pre></code>
