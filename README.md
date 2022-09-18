Proxmox: PCIe Passthrough
=========================

An ansible role that configure pci passthrough on a Proxmox host.

Requirements
------------

N/A.

Role Variables
--------------

*Required Variables*:

|  Variable  |   Default   |                       Description                       |
| :--------: | :---------: | :-----------------------------------------------------: |
|   `boot`   | `UNDEFINED` | which system you are using to boot: `grub` or `systemd` |
| `cpu_type` | `UNDEFINED` |         The CPU manufacturer: `intel` or `amd`          |

*Optional Variables*:

|      Variable       |                      Default                      |                                 Description                                 |
| :-----------------: | :-----------------------------------------------: | :-------------------------------------------------------------------------: |
|   `vfio_modules`    | `[vfio, vfio_iommu_type1, vfio_pci, vfio_virqfd]` |                      A list of kernel modules to load                       |
| `blacklist_drivers` |            `[nvidia, nouveau, radeon]`            |                       A list of drivers to blacklist                        |
|      `gpu_ids`      |                    `UNDEFINED`                    | A comma separated list of pci ids for the GPUs that will be passed through. |

Dependencies
------------

N/A.

Example Playbook
----------------

``` yml
---
- hosts: all
  remote_user: root

  roles:
    - role: mirceanton.proxmox_pci_passthrough
      vars:
        cpu_type: intel
        extra_cmdline: pcie_acs_override=downstream pcie_acs_override=multifunction nofb nomodeset video=vesafb:off video=efifb:off
        boot: systemd
        gpu_ids: 10de:1e84,10de:10f8,10de:1ad8,10de:1ad9,10de:1c81,10de:0fb9
```

MIT

Author Information
------------------

A role developed by [Mircea-Pavel ANTON](https://www.mirceanton.com).
