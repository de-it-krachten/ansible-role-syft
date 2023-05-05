[![CI](https://github.com/de-it-krachten/ansible-role-syft/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-syft/actions?query=workflow%3ACI)


# ansible-role-syft

Installs syft, CLI tool and library for generating a Software Bill of Materials from container images and filesystems<br>
https://github.com/anchore/syft<br>



## Dependencies

#### Roles
- deitkrachten.cron
- deitkrachten.logrotate

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
- Fedora 36
- Fedora 37

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# Remove syft
syft_removal: false

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

# File/directory location for Syft output
syft_log_dir: /var/log/syft
syft_log_file: syft.json

# Syft execution details
syft_wrapper_script: /usr/local/bin/syft.sh
## syft_execution_command: "{{ syft_path }} / -q --output=json --file {{ syft_log_dir }}/{{ syft_log_file }}"
syft_excludes:
  - './tmp'
syft_execution_user: root
syft_execution_group: root

# Syft schedule defaults
syft_schedule: false
syft_schedule_times:
  weekday: '*'
  hour: '01'
  minute: '00'

# Execute syft immediately
syft_immediate: false

# Central location to store all servers sbom files
syft_central_path: /var/log/syft/central

# Syft outout formats
syft_output:
  json:
    format: json
    file: syft.json
  spdx:
    format: spdx-json
    file: syft.spdx.json
  cyclonedx:
    format: cyclonedx-json
    file: syft.cyclonedx.json
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'syft'
  hosts: all
  become: "yes"
  vars:
    syft_schedule: True
    syft_immediate: True
  roles:
    - deitkrachten.cron
    - deitkrachten.logrotate
  tasks:
    - name: Include role 'syft'
      ansible.builtin.include_role:
        name: syft
</pre></code>
