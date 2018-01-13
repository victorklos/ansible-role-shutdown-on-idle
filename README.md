
# Ansible role for an on-demand server

Meaning a server that is started on-demand (through Wake-on-LAN) and powers
off after the work is done. Ideal for special-purpose servers with few users,
like my deep learning/blender server.

## Features

This ansible role:

- forces auto-logout on inactive shells
- uses `systemd` timers to periodically
- monitor ssh connections, CPU and GPU load
- shuts down the server when it is idling too long

Suitable for headless servers.


## Example playbook

```yaml
- hosts: all

  vars:
    ondemand_server_verbose: yes
    ondemand_server_shell_timeout: 1800
    ondemand_server_max_idle_time: 1800

  roles:
    - https://github.com/victorklos/ondemand-server
```


## Supported role variables

See example playbook above, default values as indicated.


## Notes

The timing defaults above make the server halt somewhere between 30 minutes
(`max_idle_time`) and 64 minutes (`shell_timeout` + `max_idle_time`) after last
use.


## Licence

MIT
