Proxmox: PCIe Passthrough
=========================

An ansible role that configure pci passthrough on a Proxmox host.

Requirements
------------

N/A.

Role Variables
--------------

|                  Variable                   |           Default           |                                 Description                                 |
| :-----------------------------------------: | :-------------------------: | :-------------------------------------------------------------------------: |
| `proxmox_pci_passthrough_blacklist_drivers` | `[nvidia, nouveau, radeon]` |                       A list of drivers to blacklist.                       |
|      `proxmox_pci_passthrough_gpu_ids`      |         `UNDEFINED`         | A comma separated list of pci ids for the GPUs that will be passed through. |

To check the default variables, take a look at the [defaults](defaults/main.yml) file.

> Note: The roles defined in the dependencies can also have their variables customized. Take a look at their readmes for more information.

Dependencies
------------

- [proxmox_iommu](https://github.com/mirceanton/ansible_role-proxmox_iommu)
- [proxmox_vfio](https://github.com/mirceanton/ansible_role-proxmox_vfio)
- [proxmox_driver_blacklist](https://github.com/mirceanton/ansible_role-proxmox_driver_blacklist)

Example Playbook
----------------

``` yml
---
- name: Enable GPU Passthrough on a PVE host
  hosts: gpupve
  remote_user: root

  roles:
    - role: mirceanton.proxmox_pci_passthrough
      vars:
        proxmox_pci_passthrough_blacklist_drivers: [ nvidia, nouveau ]
        proxmox_pci_passthrough_gpu_ids: 10de:1e84,10de:10f8,10de:1ad8,10de:1ad9,10de:1c81,10de:0fb9
```

LICENSE
-------

MIT

Author Information
------------------

A role developed by [Mircea-Pavel ANTON](https://www.mirceanton.com).
