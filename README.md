# Ansible Role: Mythic Teamserver ([Ludus](https://ludus.cloud))

An Ansible role that installs and spins up a Mythic Teamserver on a Debian or Ubuntu server. The role automatically installs a couple of Mythic agents but feel free to fork to add for your own use.

## Dependencies

None.

## Example Playbook

```yaml
- hosts: mythic_teamserver_host
  roles:
    - whispergate.ludus_mythic_teamserver
```

## Example Ludus Range Config

```yaml
ludus:
  - vm_name: "{{ range_id }}-mythic-teamserver"
    hostname: "{{ range_id }}-mythic"
    template: debian-12-x64-server-template
    vlan: 20
    ip_last_octet: 2
    ram_gb: 4
    cpus: 4
    linux: true
    testing:
      snapshot: false
      block_internet: false
    roles:
      - whispergate.ludus_mythic_teamserver
```

## License

[//]: # (If you change the License type, be sure to change the actual LICENSE file as well)
GPLv3

## Author Information

This role was created by [0xRedpoll](https://github.com/0xRedpoll), for [Ludus](https://ludus.cloud/).
