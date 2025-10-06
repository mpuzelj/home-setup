# Home Network and Home Lab Redesign Planning

## 1. Goals
- Host services with Docker or Kubernetes.
- Set up a file share for home movies, music, ISOs, etc.
- Create an ad-hoc share folder for random files.
- Provide access to services from outside the network.
- Host a torrent client in a container.
- Configure routing to use WireGuard VPN.
- Set up the network router to connect to the landlord's router and then to the internet.
- Host a private cloud.
- Configure MikroTik RB4011iGS as the WireGuard server for simplicity and reliability.
- Integrate home lab with Azure Arc for managing VMs and Kubernetes.
- Set up GitLab for CI/CD pipelines and runners.
- Configure a VM to host GitLab Runner, Azure DevOps agent, and GitHub Actions runner.

---

## 2. Current Setup Assessment
- **Landlord's Router**: SonicWall firewall/router.
- **Your Equipment**:
  - MikroTik router for primary network management.
  - Tenda router to extend Wi-Fi signal.
  - Home server for hosting VMs, containers, and file shares (OS to be selected).
- **Planned Usage**:
  - Run virtual machines (VMs) on the home server.
  - Host containers for services.
  - Set up a file share for centralized storage.
  - Use WireGuard for secure remote access.
  - Integrate with Azure Arc for managing resources.

---

## 3. Decisions and Options

### 3.1 Virtualization Host
- **Decisions**:
  - Proxmox VE: Dedicated virtualization OS.
  - Fedora/Arch with KVM: General-purpose OS with virtualization tools.
  - Other GUI-based solutions: VMware ESXi, XCP-ng, or Ubuntu Server with Cockpit.
- **Next Steps**:
  - Evaluate based on ease of use, GUI availability, and resource requirements.

### 3.2 File Sharing
- **Decisions**:
  - TrueNAS: Robust NAS solution with granular permissions.
  - Samba: Lightweight SMB sharing.
  - Nextcloud: Private cloud with advanced sharing options.
- **Next Steps**:
  - Test compatibility with older TVs, Android, Windows, and Linux.
  - Configure folders: Video, ISOs, torrent, tools, temp, and general share.

### 3.3 Subdomain Management
- **Decisions**:
  - Manage subdomains via registrar’s DNS tools.
  - Point subdomains (e.g., `vpn.wolf.3ranger.eu`) to the landlord’s static IP.
  - Use port forwarding to direct traffic to internal services.
- **Next Steps**:
  - Define subdomains and configure DNS records.
  - Set up port forwarding for each service.

### 3.4 CI/CD Tools
- **Decisions**:
  - GitLab CE: Self-hosted CI/CD platform.
  - Azure DevOps: Free tier with self-hosted agents.
  - GitHub Actions: Self-hosted runners for GitHub workflows.
- **Next Steps**:
  - Set up GitLab CE in a container or VM.
  - Configure GitLab Runner, Azure DevOps agent, and GitHub Actions runner on the same VM.

### 3.5 Azure Arc Integration
- **Decisions**:
  - Register VMs with Azure Arc for management.
  - Set up Kubernetes on VMs and integrate with Azure Arc.
- **Next Steps**:
  - Explore Azure Arc features for monitoring and deployment.
  - Test integration with Kubernetes and VMs.

---

## 4. Testing and Validation
- Test traffic forwarding and domain configuration.
- Verify WireGuard connectivity.
- Test file sharing and hosted services.
- Validate CI/CD pipelines and Azure Arc integration.