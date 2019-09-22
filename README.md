[![](https://github.com/MonolithProjects/ansible-hassio/workflows/Test%20build/badge.svg)](https://github.com/MonolithProjects/ansible-hassio/actions)  

This Ansible role installs Hass.io. Hass.io is an operating system that will take care of installing and updating Home Assistant, is managed from the Home Assistant UI, allows creating/restoring snapshots of your configuration and can easily be extended using Hass.io add-ons including Google Assistant and Let’s Encrypt.

### Playbook example:
```
---
- name: Install Hassio
  hosts: all
  become: yes
  gather_facts: no
  vars:
    - supervisor_share: "/usr/share/hassio"   #Default
    - privileged_mode: False   #Default
    - version: latest   #Default

  roles:
     - monolithprojects.hassio
```

## Requirements
```
docker-ce
avahi
dbus
```
**Note:** This Ansible role is currently only for systems with x86_64 CPU architecture


## License:
- MIT  
