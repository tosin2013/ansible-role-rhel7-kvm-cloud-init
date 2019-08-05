Deploy Red Hat KVM Image using cloud-init
=========

The following role will deploy a Red Hat Enterprise Linux 7.x KVM.

Requirements
------------
* kvm packages are installed

Role Variables
--------------

|                         |                    |                       |                                                                                                         | 
|-------------------------|--------------------|-----------------------|---------------------------------------------------------------------------------------------------------| 
| Variables               | Required           | Default               | Description                                                                                             | 
| admin_user              | x                  | admin                 | User cloud-init creates                                                                                 | 
| admin_user_password     | :heavy_check_mark: | see defaults/main.yml | Password for the cloud-init user                                                                        | 
| cidata_iso_name         | x                  | cidata.iso            | name of the iso created for cloud-init                                                                  | 
| cloud_init_iso_image    | x                  | see defaults/main.yml | full path where the cloud-init iso is stored                                                            | 
| cloud_init_meta_data    | x                  | see defaults/main.yml | full path to cloud-init meta data file                                                                  | 
| cloud_init_user_data    | x                  | see defaults/main.yml | full path to cloud-init user data file                                                                  | 
| cloud_init_vm_image     |                    |                       | name of the qcow OS iso                                                                                 | 
| disk_opt                | x                  | see defaults/main.yml | options to pass to qemu-img                                                                             | 
| disk_sequence           |                    | see defaults/main.yml | "template to generate disk device names, e.g. vdc"                                                      | 
| dns_servers             |                    |                       | dns servers for /etc/resolv manged by cloud-init                                                        | 
| extra_disk_name         |                    |                       | generated prefix for extra disk name                                                                    | 
| extra_storage           |                    |                       | "dictionary of extra disk, see defaults/main.yml"                                                       | 
| kvm_install_host        |                    | localhost             | "kvm host to run these tasks on, for future use."                                                       | 
| kvm_vm_pool_dir         | :heavy_check_mark: |                       | the libvirt pool where VM images are stored                                                             | 
| kvm_vm_root_pwd         |                    | see defaults/main.yml | sets root's password when cloud-init is executed                                                        | 
| vm_virtinstall_net_opts |                    |                       | Libvirt network with opitions that VMs will sit on                                                      | 
| manage_dns              |                    | yes                   | Enable cloud-init to setup /etc/resolv.conf                                                             | 
| os_disk                 | x                  | see defaults/main.yml | Full path to the OS primary qcow2 disk                                                                  | 
| os_qcow_template        | x                  | see defaults/main.yml | Full path to the OS qcow template                                                                       | 
| os_variant              | :heavy_check_mark: | see defaults/main.yml | Which  Linux distro                                                                                     | 
| "rhsm_activationkey     |                    |                       |                                                                                                         | 
| rhsm_org                |                    |                       |                                                                                                         | 
| rhsm_password           |                    |                       |                                                                                                         | 
| rhsm_username"          | :heavy_check_mark: | none                  | Register system to Red Hat. Use either rhsm_activationkey & rhsm_org or rhsm_password and rhsm_username | 
| search_domains          | x                  | see defaults/main.yml | sets /etc/resolv.conf search domains                                                                    | 
| vm_cpu                  | :heavy_check_mark: | see defaults/main.yml | The number of vpcu's for the VM                                                                         | 
| vm_data_dir             | :heavy_check_mark: | see defaults/main.yml | files related to VM's are stored                                                                        | 
| vm_domain               | :heavy_check_mark: | see defaults/main.yml | domain for the VM                                                                                       | 
| vm_hostname             | x                  | see defaults/main.yml |                                                                                                         | 
| vm_local_hostname       | x                  | see defaults/main.yml |                                                                                                         | 
| vm_memory               | :heavy_check_mark: | see defaults/main.yml | amount of memory for VM                                                                                 | 
| vm_name                 | :heavy_check_mark: | none                  | Short name of the vm                                                                                    | 
| vm_network_br           | :heavy_check_mark: | see defaults/main.yml | Libvirt network bridge                                                                                  | 
| vm_provision_vars       | :heavy_check_mark: | see defaults/main.yml | location for vars file created during play                                                              | 
| vm_public_key           | x                  | see defaults/main.yml | user public key                                                                                         | 
| vm_recreate             | x                  | see defaults/main.yml | recreates VM                                                                                            | 
| vm_root_disk_size       | :heavy_check_mark: | see defaults/main.yml | size of the OS root disk                                                                                | 
| vm_virtinstall_script   | :heavy_check_mark: |                       | full path to virt-install script generated                                                              | 


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------
```
- hosts: localhost
  tags: provision
  vars:
    update_inventory: true
    inventory_file: /inventory/instances/localhost
    kvm_vm_pool_dir: "/var/lib/libvirt/images"
    kvm_install_host: localhost
    vm_recreate: false
    vm_teardown: false
    cloud_init_vm_image: "rhel-server-7.6-x86_64-kvm.qcow2"
    vm_name: test0073
    vm_public_key: "{{ lookup('file', '~/.ssh/id_rsa.pub') }}"
    vm_cpu: 2
    vm_memory: 2048
    vm_root_disk_size: 20G
    vm_libvirt_net: default
    rhsm_org: "7828949"
    rhsm_activationkey: "act-os-rhel-7Server"
    admin_user_password: mypassword
    extra_storage:
      - size: 80G
        enable: true
      - size: 50G
        enable: true
  tasks:
    - name: Create KVM VM
      include_role:
        name: ansible-role-rhel7-kvm-cloud-init
```

License
-------
GPLv3


Author Information
------------------

This role was created in 2019 by [Tosin Akinosho](http://github.com/tosin2013)
