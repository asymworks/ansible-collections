# Ansible Role: Docker Server

An Ansible Role that installs the Docker Image Update Notifier (diun) service.

## Requirements

None

## Role Variables (General)

Available variables for the role are listed below, along with default values if applicable (see `defaults/main.yml`):

```yaml
diun_enabled: true
diun_tag: latest
diun_watch_schedule: 0 */6 * * *
diun_watch_stopped: true
diun_watch_workers: 20
```

Enables or disables the Diun container and configures the Diun Docker watcher.

```yaml
diun_notif_mail_host: localhost
diun_notif_mail_port: 25
diun_notif_mail_localname: "{{ ansible_hostname }}"
diun_notif_mail_from: "diun@{{ ansible_fqdn }}"
diun_notif_mail_to: "diun@localhost"
```

Configures the Diun Mail notifier.

## Role Facts

None

## Role Handlers

None

## Dependencies

| Collection | Version |
| --- | --- |
| `asymworks.core` | >= 1.0.0 |
| `asymworks.docker` | >= 1.0.0 |
| `community.docker` | >= 3.4.0 |
| `community.general` | >= 7.0.0 |

## Example Playbook

```yaml
- hosts: all
  roles:
    asymworks.core.baseline
    asymworks.docker.common
    asymworks.docker.diun
```

## License

MIT / BSD

## Author

This role was created in 2019 by Jonathan Krauss for managing home network infrastructure.
