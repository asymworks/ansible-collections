# Ansible Role: Docker Server

An Ansible Role that installs the Docker Container Server.

## Requirements

None

## Role Variables (General)

Available variables for the role are listed below, along with default values if applicable (see `defaults/main.yml`):

```yaml
docker_ipv6: false
docker_ipv6_nat: true
docker_ipv6_subnet: fd00::/80
docker_ipv6_network: default
```

Configure Docker for IPv6 operation when the `docker_ipv6` variable is truthy. This sets the `ipv6` and `fixed-cidr-v6` properties on the Docker daemon, and either installs the Docker IPv6 NAT container when `docker_ipv6_network` is `default`, or creates a new IPv6 bridge network for containers. Note that in the second mode, additional steps will be required to route network traffic to the containers, such as installing `ndppd`, which is not done automatically.

```yaml
docker_telegraf: true
```

Install the Docker input plugin for Telegraf.

```yaml
telegraf_docker_gather_services: false
telegraf_docker_containers_include: []
telegraf_docker_containers_exclude: []
telegraf_docker_timeout: 5s
telegraf_docker_stats_perdev: ["cpu","blkio","network"]
telegraf_docker_stats_total: ["cpu","blkio","network"]
```

Configuration options for the Telegraf Docker input plugin.

```yaml
docker_loki_enabled: true
docker_loki_url: https://localhost:3100/loki/api/v1/push
docker_loki_opts: {}
```

Enables or disables the global Loki logging endpoint for the Docker Daemon.
`docker_loki_opts` are written to the `log-opts` object in the `daemon.json`
file.

## Role Facts

None

## Role Handlers

None

## Dependencies

| Collection | Version |
| --- | --- |
| `asymworks.core` | >= 1.0.0 |
| `community.docker` | >= 3.4.0 |
| `community.general` | >= 7.0.0 |

## Example Playbook

```yaml
- hosts: all
  roles:
    asymworks.core.baseline
    asymworks.core.docker
```

## License

MIT / BSD

## Author

This role was created in 2019 by Jonathan Krauss for managing home network infrastructure.
