# Ansible Role: Asymworks Wireguard Client

An Ansible Role that installs the Wireguard client on Asymworks servers running Debian or Alpine Linux.

## Requirements

None

## Role Variables

Available variables are listed below, along with default values if applicable (see `defaults/main.yml`):

```yaml
wireguard_interfaces: []
```

Array of Wireguard interfaces. Each entry in the list will be set up as a `wgX.conf` file.  The array entries should have the following structure:

```yaml
# Example (from the OpnSense Road Warrior Documentation)
wireguard_interfaces:
  wg0:
    enabled: true
    state: started
    address: [ "10.10.10.2/32", "fd00:1234:abcd:ef09:10:2/128" ]
    private_key: 8GboYh0YF3q/hJhoPFoL3HM/ObgOuC8YI6UXWsgWL2M=
    dns: [ "192.168.1.254", "fd00:1234:abcd:ef09:1:254" ]
    peer:
      endpoint: opnsense.example.com:51820
      public_key: OwdegSTyhlpw7Dbpg8VSUBKXF9CxoQp2gAOdwgqtPVI=
      allowed_ips: [ "0.0.0.0/0", "::/0" ]
```

The `enabled` and `state` keys controls the corresponding service to bring the interface up and down.  The `state` key can be `started`, `stopped`, or `absent` (which will disable the service and delete the configuration file).  Note that setting the `dns` key requires that `resolvconf` is installed on the target system.  If DNS will not be provided over the Wireguard link, the key can be omitted.

## Role Facts

None

## Dependencies

This requires the `asymworks.core.baseline` role to be installed.

## Example Playbook

```yaml
- hosts: all
  pre_tasks:
    include_role:
      name: asymworks.core.baseline
      tasks_from: pre-tasks.yml
  roles:
    asymworks.core.baseline
    asymworks.core.wireguard
  post_tasks:
    include_role:
      name: asymworks.core.baseline
      tasks_from: post-tasks.yml
```

## License

MIT / BSD

## Author

This role was created in 2022 by Asymworks, LLC.
