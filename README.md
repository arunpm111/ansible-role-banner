# Ansible Role: Banner

An Ansible role to manage Linux login banners (`/etc/motd`, `/etc/issue`, `/etc/issue.net`) and optionally configure the SSH `Banner` directive.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

### Banner Content

```yaml
banner_motd: ""
```

Content for `/etc/motd` (Message of the Day), displayed after a successful login.

```yaml
banner_issue: ""
```

Content for `/etc/issue`, displayed on local terminal login screens before authentication.

```yaml
banner_issue_net: ""
```

Content for `/etc/issue.net`, displayed for network (SSH) logins before authentication.

### Banner Management Flags

```yaml
banner_motd_manage: true
banner_issue_manage: true
banner_issue_net_manage: true
```

Set any of these to `false` to skip managing the corresponding banner file.

### SSH Configuration

```yaml
banner_ssh_configure: true
```

When `true`, the role configures the `Banner` directive in `/etc/ssh/sshd_config`.

```yaml
banner_ssh_banner_path: /etc/issue.net
```

The file path used for the SSH `Banner` directive.

### Service Management

```yaml
banner_service_manage: true
```

Whether to restart the SSH service when the SSH configuration changes.

```yaml
banner_restart_handler_state: restarted
```

The desired state for the SSH service when the handler is triggered.

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  roles:
    - role: ansible-role-banner
      vars:
        banner_motd: |
          ******************************************
          *   Welcome to the managed server.       *
          *   All activity is monitored.           *
          ******************************************
        banner_issue: |
          Authorized access only.
        banner_issue_net: |
          Authorized access only. All activity is monitored and recorded.
```

## Testing

This role uses [Molecule](https://molecule.readthedocs.io/) for testing. To run the tests locally:

```bash
pip install ansible molecule molecule-plugins[docker] docker
molecule test
```

## License

MIT

## Author Information

This role was created by [arunpm111](https://github.com/arunpm111).
