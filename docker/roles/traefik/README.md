# Ansible Role: Docker Server

An Ansible Role that installs the Docker Traefik HTTP Proxy.

## Requirements

None

## Role Variables (General)

Available variables for the role are listed below, along with default values if applicable (see `defaults/main.yml`):

```yaml
traefik_enabled: false
traefik_tag: "v2.5"
traefik_domain: "{{ ansible_domain }}"
traefik_network: traefik
traefik_log_level: INFO
traefik_access_log: {}
traefik_access_log_path: /var/log/traefik
traefik_cert_resolvers: {}
traefik_yml_additional: {}
```

Configures the Traefik proxy.  The `traefik_access_log_path` will be created on the Docker host system and mapped into the Traefik container automatically.  The `traefik_access_log` and `traefik_cert_resolvers` variables are written directly to the `accessLog` and `certificateResolvers` sections of the `traefik.yml` file respectively, and can contain any valid configuration data for those sections.  The `traefik_yml_additional` is written to the `traefik.yml` file without additional translation at the top level.

```yaml
traefik_http_port: "80"
traefik_https_port: "443"
traefik_entrypoints:
  web:
    address: ":{{ traefik_http_port }}"

traefik_docker_ports:
  - "{{ traefik_http_port }}:80/tcp"
  - "{{ traefik_https_port }}:443/tcp"
```

Configures Traefik entry points.  The `traefik_entrypoint` variable content is written directly to the `entryPoints` variable in `traefik.yml` and so can contain other functionality such as enforced HTTP to HTTPS redirects.  The `traefik_docker_ports` controls the mapping of host ports to docker container ports and is passed directly to the `ports` attribute of the docker container.

```yaml
traefik_logrotate_enabled: "{{ traefik_access_log|bool }}"
```

Configures a log rotation for Traefik access logs on the host system.

```yaml
traefik_api_enabled: false
```

Enables the Traefik API and Dashboard when set to `true`.

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
    asymworks.docker.traefik
```

## License

MIT / BSD

## Author

This role was created in 2019 by Jonathan Krauss for managing home network infrastructure.
