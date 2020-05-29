# Lynis-Role

Application of Lynis audit tool suggestions.

## Requirements

none

## Role Variables

To satisfy an external logging the variable must be set to point to your syslog server in `group_vars/nodes.yml`:

```yaml
syslog_server: "log"
```

## Dependencies

none

## Example Playbook

```yaml
---
# Lyris Hardening Fixes

- name: Lyris Hardening Fixes
  hosts: nodes
  become: yes
  become_method: sudo
  roles:
    - lynis-role
```

```shell
ansible-playbook site.yml -i production -v
```

## License

GPLv3.0

# Author Information

Paul Bargewell <paul.bargewe@opusvl.com>
