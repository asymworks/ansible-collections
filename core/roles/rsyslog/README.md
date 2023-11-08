# Ansible Role: Asymworks Rsyslog

An Ansible Role that installs Rsyslog on Asymworks servers running Debian or Alpine Linux.

## Requirements

None

## Role Variables

Available variables are listed below, along with default values if applicable (see `defaults/main.yml`):

```yaml
rsyslog_enabled: true
syslog_server: logs.lan
syslog_port: 10514
```

Whether the remote `syslog` server is enabled and installe.  If enabled, logs are sent in RFC3164 format via UDP to the specified server and port so they can be parsed by e.g. Logstash or Graylog.

```yaml
rsyslog_hostname:
rsyslog_preserve_fqdn: true
```

Sets the hostname that Rsyslog reports.  If this is unset (the default), the Rsyslog default behavior will be used.  Set `rsyslog_preserve_fqdn` to `true` to have Rsyslog preserve the FQDN of the host, otherwise the short hostname will be sent.

```yaml
rsyslog_local_file: /var/log/messages
rsyslog_local_level: '*'
```

Sets the minimum log level for local logging (to `rsyslog_local_file`). By default all messages are logged locally as well as remotely. If `rsyslog_local_file` is empty, this function will be disabled and logs will not be written locally (e.g. when `journald` is used).

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
    asymworks.core.rsyslog
  post_tasks:
    include_role:
      name: asymworks.core.baseline
      tasks_from: post-tasks.yml
```

## License

MIT / BSD

## Author

This role was created in 2022 by Asymworks, LLC.
