# Ansible Role: Asymworks NFSv4 Configuration

An Ansible Role that sets up NFSv4 on Linux hosts. The default entry point installs and optionally enables NFSv4 file sharing with ID mapping (`sec=sys` mode).

## Requirements

None

## Role Variables

Available variables are listed below, along with default values if applicable (see `defaults/main.yml`):

```yaml
nfsv4_enabled: false
nfsv4_idmap_domain: "{{ ansible_domain }}"
nfsv4_idmap_service: >
  {{
    'rpc.idmapd'
      if ansible_facts['os_family']|lower == 'alpine'
      else 'nfs-idmapd' 
  }}

nfs_automount: true
```

Configures NFSv4 ID mapping and optionally enables automatic mount of NFS volumes at boot (Alpine Linux only).

## Dependencies

This requires the `asymworks.core.baseline` role to be installed.

## Additional Entry Points

None

## Example Playbook

    - hosts: all
      pre_tasks:
        include_role:
          name: asymworks.core.baseline
          tasks_from: pre-tasks.yml
      roles:
        asymworks.core.nfs4
      post_tasks:
        include_role:
          name: asymworks.core.baseline
          tasks_from: post-tasks.yml

## License

MIT / BSD

## Author

This role was created in 2023 by Asymworks, LLC.
