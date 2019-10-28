Role rhel_vmware_disk_manager
=============================

1- Added disk vmware, partition, lvg, lvol, format, mount and * extend * lv for rhel 7 and 8 (option a or b or c or d or e or f)  
2- Existing LV / mountpoint extension. the vg in question must have enough space, please check before (option g)

Required
--------

Have access to the python API vmware pyvmomi  
Have the latest copy of vmware_guest_disk_facts_beta.py  
Limit ansible must be the server in question (with FQDN)  
The os system disk must be scsi_id: 0 and unit_number: 0 (default)  

Dependences
------------

None

Limitations
-----------

Set_fact tasks have "ignore_errors: true". set_fact is not ignored if option g  
Existing LV / mountpoint extension (option g), the vg in question must have enough space  
Only 4 SCSI controllers are allowed per virtual machine.  
You must take precautions when specifying scsi_controller = 0 and unit_number = 0 because this disk may contain an operating system.  
The os system disk must be scsi_id: 0 and unit_number: 0 (default)  
unit_number (integer): disk unit number. Valid values ​​range from 0 to 15. Only 15 disks are allowed per SCSI controller.  

Client variables
----------------

The following variables can be defined by the customer

| Variable                                       | Example     | Comments (type)                                              |  
| : ---                                          | : ---       | : ---                                                        |  
| `rhel_vmware_disk_manager__vmdisk_name`        | serverx     | Server name (without FQDN)                                   |  
| `rhel_vmware_disk_manager__vmdisk_size_gb`     | 100         | Disk size in gig                                             |  
| `rhel_vmware_disk_manager__lv_size_gb`         | 96          | Space in gig at the end of the LV                            |  
| `rhel_vmware_disk_manager__vmdisk_vg_name`     | domvg006    | VG's name (vgappl or system most of the time)                |  
| `rhel_vmware_disk_manager__vmdisk_lv_name`     | domlv006    | Name of the LV. EX: "lvoptvmware" for /opt/vmware            |  
| `rhel_vmware_disk_manager__vmdisk_path_name`   | /dompath006 | The path for the mountpoint. EX: for /opt/vwware             |  
| `rhel_vmware_disk_manager__vmdisk_path_option` | defaults    | mp opts Ex:"rw, relatime, seclabel, attr2, inode64, noquota" |  
| `rhel_vmware_disk_manager__vmdisk_fs_type`     | xfs         | Type of filesystem (xfs most of the time) eg ext4 or xfs     |  
| `rhel_gestion_disk_vmware__options`            | f           | User choice  a-b-c-d-e-f-g                                   |  

```
POSSIBLE CHOICE:  
a: Adding a disk (raw device)
b: Adding a disk + partition
c: Adding a disk + partition + add the disk to the requested VG
d: Addition of a disk + partition + add the disk to the requested VG + Creation of the requested LV
e: Adding a disk + partition + adding the disk to the requested VG + Creating the requested LV + formatting the filesystem
f: Adding a disk + partition + adding the disk to the requested VG + Creating the requested LV + formatting the filesystem + mount the mountpoint
g: Existing mountpoint only (the vg in question must have enough space, please check before) LVEXTEND
```

For other variables for the role, see the file defaults / main.yml  

Author
------

Dominic D'Apice (https://github.com/dapiced)  

Reference
---------

[Https://docs.ansible.com/ansible/latest/modules/vmware_guest_disk_module.html]  
[Https://docs.ansible.com/ansible/latest/modules/vmware_guest_disk_facts_module.html]  
[https://github.com/ansible/ansible/pull/58117/files] (vmware_guest_disk_facts_module beta)  
[Https://docs.ansible.com/ansible/latest/modules/vmware_vm_facts_module.html]  
