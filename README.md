# Role Name

`ansible-opcli` is an Ansible role which deploys 1Password client (`op`) on a host

# Requirements

Ubuntu 22.04 tested

# Role Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `repo_arch` | `amd64` | Architecture of the dpkg |
| `op_repo` | `deb [arch={{ repo_arch }} signed-by=/usr/share/keyrings/1password-archive-keyring.gpg] https://downloads.1password.com/linux/debian/{{ repo_arch }} stable main` | 1Password repository URL |
| `op_repo_key` | `https://downloads.1password.com/linux/keys/1password.asc` | 1Password repository key URL |
| `op_rpm_key_url` | `https://downloads.1password.com/linux/keys/1password.asc` | 1Password repository key URL for RPM/YUM |
| `op_repo_state` | `present` | Whether the repository should be present or absent |
| `op_inject_user` | `""` | User to inject the service account token to |
| `op_service_account_token` | `""` | Service account token |
| `op_inject_path` | `/home/{{ op_inject_user }}/.op` | Path where the service account token will be injected |
| `op_cli_install_method` | `repo` | Install method: `repo` (default, repository), `deb` (download .deb), `none` (skip install) |
| `op_cli_absent` | `false` | Uninstall 1Password CLI if set to `true` |

# Dependencies

- `ansible.builtin`
- `community.general` (for Alpine support)

# Supported Platforms

- Debian/Ubuntu (APT or direct .deb)
- RedHat/CentOS/EL (YUM/DNF or direct .rpm)
- Alpine Linux (APK)

Tested on Ubuntu 24.04 and Rocky Linux 9

# Example Playbook

    - hosts: all
      roles:
         - ansible-opcli

    - hosts: all
      become: true
      roles:
         - role: ansible-opcli
           vars:
             op_inject_user: "myuser"
             op_service_account_token: "mytoken"
             op_inject_path: "/custom/path/.op"
