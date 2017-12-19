## Overview

A simple Ansible script to extend Logical Volume as a new disc is attached to a remote server. This is required particularly when our K8S cluster nodes will be required to extend their storage therby adding new discs.

The script here leverages `lvm` family commands to do its job. The approach:

- check if the Physical Volume (PV) exists and is part of a Virtual Group (VG) as mentioned in the configurations
- check if there is enough space to create / extend Logical Volumes (LV) in that PV
- create or extend LV with exact new size i.e. if the current size of the LV is 2GB and it needs extension of 50GB then the size to be mentioned in the configuration would be 52GB.
- ther is a redundant check to see if the FileSystem (FS) needs resizing
- create/resize FS to match the new LV size (using `resizefs`) and mount it in the path mentioned in the configuration

## Configuration

Make sure to change the relevant details in the configuration files located inside `inventory` folders. Also the host ip like senstive data is placed inside `inventory/group_vars/all/vault.yml` that need to be updated before executing the playbook.

## Playbook Execution

```
$ ansible-playbook -i inventory/hosts.cfg -kK -v --ask-vaullt-pass playbook.yml
```
