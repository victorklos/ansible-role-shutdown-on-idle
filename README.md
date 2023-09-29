# This project is archived

Feel free to fork.

---

[![Build Status](https://travis-ci.org/victorklos/ansible-role-shutdown-on-idle.svg?branch=master)](https://travis-ci.org/victorklos/ansible-role-shutdown-on-idle)

# Ansible role to shutdown a server after the work is done.

This role installs a systemd service with timer that monitors a server for
activity and shuts it down after it has been idling for a specific period.
Ideal for special-purpose servers with few users, like my deep learning/blender
server.

## Features

This ansible role:

- uses `systemd` timers to periodically
- monitor ssh connections, CPU and GPU load
- shuts down the server when it is idling too long

Suitable for headless servers.


## Example playbook

```yaml
- hosts: all

  vars:
    shutdown_on_idle_max_idle_time: 1800

  roles:
    - victorklos.shutdown-on-idle
```


## Supported role variables

See example playbook above, default value as indicated.


## Notes

Remember to also kick inactive ssh users or otherwise the host will never be
considered idle.

You can see what is going on by issueing one of these:

    systemctl status shutdown_on_idle.timer             # the timer part
    systemctl status shutdown_on_idle.service           # the monitoring part
    journalctl --boot --unit=shutdown_on_idle.service   # all logs since boot


## Licence

MIT
