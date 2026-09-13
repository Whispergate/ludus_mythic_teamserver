# Ansible Role: Mythic Teamserver ([Ludus](https://ludus.cloud))

An Ansible role that installs and spins up a Mythic Teamserver on a Debian or Ubuntu server. Mythic agents and C2 profiles are configurable via `role_vars` — specify any GitHub repos you want installed.

## Role Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `ludus_mythic_agents` | See below | List of GitHub repo URLs for Mythic agents to install |
| `ludus_mythic_c2_profiles` | See below | List of GitHub repo URLs for Mythic C2 profiles to install |
| `ludus_mythic_bind_localhost_only` | `false` | Bind Mythic server to localhost only (set `true` to restrict access) |
| `ludus_mythic_dynamic_ports_bind_localhost_only` | `false` | Bind SOCKS proxy ports to localhost only |

### Default Agents

```yaml
ludus_mythic_agents:
  - https://github.com/MythicAgents/Apollo
  - https://github.com/MythicAgents/forge
  - https://github.com/MythicAgents/service_wrapper
  - https://github.com/Whispergate/Starburst
  - https://github.com/Whispergate/Erebus
  - https://github.com/Whispergate/Ariadne
  - https://github.com/Whispergate/Sphinx
  - https://github.com/Whispergate/Daedalus
```

### Default C2 Profiles

```yaml
ludus_mythic_c2_profiles:
  - https://github.com/MythicC2Profiles/http
  - https://github.com/MythicC2Profiles/smb
```

## Dependencies

None.

## Example Playbook

```yaml
- hosts: mythic_teamserver_host
  roles:
    - whispergate.ludus_mythic_teamserver
```

## Example Ludus Range Config

### Default (all built-in agents and profiles)

```yaml
ludus:
  - vm_name: "{{ range_id }}-mythic"
    hostname: "{{ range_id }}-mythic"
    template: ubuntu-24.04-x64-server-template
    vlan: 99
    ip_last_octet: 6
    ram_gb: 16
    cpus: 8
    linux: true
    roles:
      - whispergate.ludus_mythic_teamserver
```

### Custom agents and profiles

```yaml
ludus:
  - vm_name: "{{ range_id }}-mythic"
    hostname: "{{ range_id }}-mythic"
    template: ubuntu-24.04-x64-server-template
    vlan: 99
    ip_last_octet: 6
    ram_gb: 16
    cpus: 8
    linux: true
    roles:
      - whispergate.ludus_mythic_teamserver
    role_vars:
      ludus_mythic_agents:
        - https://github.com/MythicAgents/Apollo
        - https://github.com/MythicAgents/poseidon
        - https://github.com/MythicAgents/merlin
      ludus_mythic_c2_profiles:
        - https://github.com/MythicC2Profiles/http
        - https://github.com/MythicC2Profiles/websocket
```

### Minimal (no agents, no profiles)

```yaml
ludus:
  - vm_name: "{{ range_id }}-mythic"
    hostname: "{{ range_id }}-mythic"
    template: ubuntu-24.04-x64-server-template
    vlan: 99
    ip_last_octet: 6
    ram_gb: 16
    cpus: 4
    linux: true
    roles:
      - whispergate.ludus_mythic_teamserver
    role_vars:
      ludus_mythic_agents: []
      ludus_mythic_c2_profiles: []
```

## License

GPLv3

## Author Information

This role was created by [0xRedpoll](https://github.com/0xRedpoll) and modified by [Whispergate](https://github.com/Whispergate), for [Ludus](https://ludus.cloud/).
