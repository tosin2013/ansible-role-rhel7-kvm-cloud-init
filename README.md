This role deploys a Libvirt KVM instance from a qcow image
=========

Tested deployments:
 - Red Hat Enterprise Linux 7/8
 - Fedora

Requirements
------------
* kvm packages are installed

Role Variables
--------------
Please see defaults/main.yml

Dependencies
------------
N/A

Example Playbooks
-----------------

**Deploy Fedora**
```
- name: Fedora VM
  hosts: localhost
  become: yes

  vars:
    vm_name: "fedora32"
    vm_cpu: "2"
    vm_memory: "2048"
    vm_root_disk_size: "20G"
    vm_teardown: no
    vm_qcow_image: Fedora-Cloud-Base-32-1.6.x86_64.qcow2
    admin_user: changeme
    admin_user_password: changeme
    kvm_vm_root_pwd: changeme
    os_release: fedora31
    

  tasks:
    - name: deploy a kvm node
      include_role:
        name: deploy-kvm-vm
```

**Deploy RHEL 8**
```
- name: Deploy RHEL 8.3 Beta VM
  hosts: localhost
  become: yes

  vars:
    vm_name: "rhel83-beta"
    vm_cpu: "2"
    vm_memory: "2048"
    vm_root_disk_size: "20G"
    vm_teardown: no
    vm_qcow_image: rhel-8.3-beta-1-x86_64-kvm.qcow2
    admin_user: changeme
    admin_user_password: changeme
    kvm_vm_root_pwd: changeme
    os_release: rhel8.2
    rhsm_activationkey: rhel-server
    rhsm_org: 1234565


  tasks:
    - name: deploy a kvm node
      include_role:
        name: deploy-kvm-vm
```

License
-------
GPLv3


Author Information
------------------

This role was created in 2019 by [Tosin Akinosho](http://github.com/tosin2013)
