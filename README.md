# Kasm server installation
[Kasm](https://www.kasmweb.com/) is desktop and browser isolation platform.  

This role will search for running Kasm docker containers. If there are not any, role will install Kasm server. Optionally it can create a persistent storage for home folder of 5 users per one server (Community Kasm version allows maximum of 5 user sessions on one server)

### Quick guide

1. register at https://www.kasmweb.com/downloads.html and download the latest community version of the Kasm Server and place it into `playbooks/files/` directory
2. define kasm servers in `inventory/hosts.ini`
3. run `ansible-galaxy install -r inventory/requirements.yml`
4. run `ansible-playbook site.yml`
5. see the Kasm credentials in the ansible output. Login into the Kasm server WebUI (output of the installation log is in `~/kasm.log`)...
---

### Playbook example:
```
---
- name: Install KASM server with persistent storage
  hosts: kasm_servers
  become: yes
  gather_facts: no

  vars:
     - kasm_package: kasm_release_1.5.0.3b363e.tar.gz
     - kasm_user_name: user
     - display_creds: True
     - persistent_storage: True

  roles:
     - ansible-kasm_server
```
---

### Manual steps for Kasm server configuration for persistent home folder

#### Create users:
Login to the Kasm WebUI and create users called `<kasm_user_name>[1-5]` (5 users per one Kasm server. For example in case of 2 Kasm servers, create `user[1-10]`)

#### Create a new image for each user:
Each user will need it's own Kasm image to have persistent home folder.
For each image setup the volume mapping.

**Volume Mappings (JSON)**
```
{"/home/<replace for ansible_user>/share/<replace for kasm_user_name+index number>":{"mode":"rw","bind":"/home/kasm-user"}}
```

### Requirements:
- docker
- docker-compose
- swap enabled

### License:
- MIT
