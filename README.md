Proxmox: PCIe Passthrough
=========================

An ansible role that configure pci passthrough on a Proxmox host.

Requirements
------------

N/A.

Role Variables
--------------

**Required Variables**:

|              Variable               |        Type         |   Default   |                           Description                            |
| :---------------------------------: | :-----------------: | :---------: | :--------------------------------------------------------------: |
| `proxmox_pci_passthrough_boot_type` | `grub` or `systemd` | `UNDEFINED` | which system you are using to proxmox_pci_passthrough_boot_type. |
| `proxmox_pci_passthrough_cpu_type`  |  `intel` or `amd`   | `UNDEFINED` |                      The CPU manufacturer.                       |

**Optional Variables**:

|                  Variable                   |                      Default                      |                                 Description                                 |
| :-----------------------------------------: | :-----------------------------------------------: | :-------------------------------------------------------------------------: |
|   `proxmox_pci_passthrough_vfio_modules`    | `[vfio, vfio_iommu_type1, vfio_pci, vfio_virqfd]` |                      A list of kernel modules to load                       |
| `proxmox_pci_passthrough_blacklist_drivers` |            `[nvidia, nouveau, radeon]`            |                       A list of drivers to blacklist                        |
|      `proxmox_pci_passthrough_gpu_ids`      |                    `UNDEFINED`                    | A comma separated list of pci ids for the GPUs that will be passed through. |
|   `proxmox_pci_passthrough_extra_cmdline`   |                    `UNDEFINED`                    |             Extra parameters to be added to the kernel cmdline.             |

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
        proxmox_pci_passthrough_boot_type: systemd
        proxmox_pci_passthrough_cpu_type: intel
        proxmox_pci_passthrough_gpu_ids: 10de:1e84,10de:10f8,10de:1ad8,10de:1ad9,10de:1c81,10de:0fb9
        proxmox_pci_passthrough_extra_cmdline: pcie_acs_override=downstream pcie_acs_override=multifunction nofb nomodeset video=vesafb:off video=efifb:off video=simplefb:off initcall_blacklist=sysfb_init vga=off
```

MIT

Author Information
------------------

A role developed by [Mircea-Pavel ANTON](https://www.mirceanton.com).
