# Home Server Setup

## Select Operating System
- **Options**:
  - Proxmox VE: Dedicated virtualization OS.
  - Fedora/Arch with KVM: General-purpose OS with virtualization tools.
  - Other GUI-based solutions: VMware ESXi, XCP-ng, or Ubuntu Server with Cockpit.
- **Next Steps**:
  - Evaluate based on ease of use, GUI availability, and resource requirements.

## Configure Virtual Machines
- **Objective**: Set up VMs for specific tasks.
- **Steps**:
  1. Install and configure the hypervisor.
  2. Create VMs for:
     - Private cloud.
     - Torrent client.
     - Other services.
  3. Register VMs with Azure Arc for management.

## Set Up Containers
- **Objective**: Host services using Docker or Kubernetes.
- **Steps**:
  1. Install Docker or Kubernetes.
  2. Deploy containers for:
     - File sharing.
     - Media servers.
     - Other applications.
  3. Set up Kubernetes on VMs and integrate with Azure Arc.

## File Sharing
- **Options**:
  - TrueNAS: Robust NAS solution with granular permissions.
  - Samba: Lightweight SMB sharing.
  - Nextcloud: Private cloud with advanced sharing options.
- **Next Steps**:
  - Test compatibility with older TVs, Android, Windows, and Linux.
  - Configure folders: Video, ISOs, torrent, tools, temp, and general share.