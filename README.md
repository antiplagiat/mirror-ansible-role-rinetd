# ansible-rinetd

## Overview

Ansible role - install and configure rinetd service.  

Tasks:  

  - install rinetd
  - configure rinetd (`/etc/rinetd.conf`)
  - restart rinetd service

## Getting started with an example

### Configure

Edit `rinetd/vars/main.yml`:  

```yaml
---
# vars file for rinetd
allowedhosts:
  - comment: 'workspace'
    hosts:
      - 192.168.0.*
      - 192.168.1.10
redirections:
  - comment: 'webserver'
    connectaddress: 192.168.0.11
    ports:
      - connectport: 22
        bindport: 2200
      - connectport: 80
        bindport: 8000
      - connectport: 443
        bindport: 44300
```

### Run

`playbook.yml`:  

```yaml
- hosts: localhost
  connection: local

  roles:
    - rinetd
```

Running playbook:  

```bash
ansible-playbook playbook.yml
```

### Result

Rinetd configuration:  

```

# workspace
allow 192.168.0.*
allow 192.168.1.10

#
# bindaddress    bindport  connectaddress  connectport

# webserver
192.168.0.24	2200	192.168.0.11	22
192.168.0.24	8000	192.168.0.11	80
192.168.0.24	44300	192.168.0.11	443

# logging information
logfile /var/log/rinetd.log
```

## Licence

GNU General Public License v3 (GPL-3). See `LICENSE` for further details.
