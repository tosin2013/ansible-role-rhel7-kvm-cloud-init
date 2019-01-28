Deploy Red Hat KVM Image using cloud-init
=========

The following role will deploy a Red Hat Enterprise Linux 7.x KVM.

Requirements
------------
* kvm packages are installed

Role Variables
--------------

Populate values in vars/main.yml

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------
```
---
- hosts: localhost
  remote_user: root
  roles:
    - ansible-role-rhel7-kvm-cloud-init
```

License
-------
GPLv3


Author Information
------------------

This role was created in 2019 by [Tosin Akinosho](http://github.com/tosin2013)
