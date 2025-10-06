# Work Plan for Home Network and Lab Setup

## 1. Upstream Planning

### 1.1 Coordinate with Landlord's IT
- **Objective**: Forward specific traffic from the landlord's SonicWall router to your MikroTik router.
- **Steps**:
  1. Request the landlord's IT to forward traffic to your router's IP address.
  2. Decide on traffic filtering:
     - Option 1: Forward all traffic for your domain `3ranger13.eu` to your router.
     - Option 2: Forward all traffic via WireGuard VPN (requires one UDP port to be forwarded).
  3. Provide the necessary details to the landlord's IT:
     - Your router's IP address.
     - The domain name or specific ports to forward.

### 1.2 Domain Configuration
- **Objective**: Configure `3ranger13.eu` to route traffic to your network.
- **Steps**:
  1. Update DNS records to point to the landlord's public IP address.
  2. Ensure traffic is forwarded to your MikroTik router.

### 1.3 Traffic Forwarding Plan
- **Objective**: Forward internet and WireGuard traffic from the landlord's SonicWall to your MikroTik router.
- **Steps**:
  1. **Landlord's SonicWall Configuration**:
     - Request forwarding of all traffic for `wolf.3ranger.eu` to your MikroTik router's WAN IP (`192.168.5.x`).
     - Alternatively, request port forwarding for specific services:
       - HTTP/HTTPS traffic for hosted services.
       - UDP port `51820` for WireGuard VPN.
  2. **MikroTik Configuration**:
     - Set up the WAN port to use DHCP to obtain an IP in the `192.168.5.x` subnet.
     - If possible, request a static IP (e.g., `192.168.5.10`) for stability.
     - Configure NAT and firewall rules to allow incoming traffic from the SonicWall.
  3. **Testing**:
     - Verify that traffic to `wolf.3ranger.eu` reaches your MikroTik router.
     - Test access to hosted services and WireGuard VPN.

---

## 2. Router Configuration

### 2.1 MikroTik Router
- **Objective**: Set up the MikroTik router to handle incoming traffic.
- **Steps**:
  1. Configure NAT rules to forward traffic to appropriate devices/services.
  2. Set up WireGuard VPN for secure remote access.
  3. Implement firewall rules to secure the network.

### 2.2 Tenda Router
- **Objective**: Extend Wi-Fi coverage.
- **Steps**:
  1. Configure the Tenda router as an access point.
  2. Connect it to the MikroTik router.

---

## 3. WireGuard Setup

### 3.1 Decide on WireGuard Server Location
- **Options**:
  - **Home Lab Server**:
    - Preferred option: Run WireGuard in a container on the home lab server.
    - Considerations:
      - Ensure traffic can pass through the SonicWall router correctly.
      - Coordinate with landlord's IT to forward the required UDP port.
  - **Oracle Cloud VM**:
    - Alternative option: Host WireGuard on the free Oracle Cloud VM.
    - Considerations:
      - Public IP simplifies traffic forwarding.
      - May require additional configuration for integration with the home network.

### 3.2 Configure WireGuard
- **Objective**: Provide secure access to your network for personal and friends' devices.
- **Steps**:
  1. Install WireGuard on the chosen server (home lab or Oracle Cloud).
  2. Generate keys for:
     - Your devices (e.g., laptop, phone).
     - Friends' devices (e.g., computers, phones).
  3. Configure WireGuard peers for each device.
  4. Set up routing to allow access to:
     - Home network services.
     - Internet traffic (if desired).

### 3.3 Test and Validate
- **Objective**: Ensure WireGuard is functioning as expected.
- **Steps**:
  1. Test connectivity from your devices (laptop, phone).
  2. Test connectivity from friends' devices.
  3. Verify access to home network services and internet.

### 3.4 MikroTik as WireGuard Server
- **Objective**: Use the MikroTik RB4011iGS as the WireGuard server for simplicity and reliability.
- **Steps**:
  1. **Update RouterOS**:
     - Ensure the MikroTik router is running RouterOS 7.1 or later.
  2. **Create WireGuard Interface**:
     - Add a new WireGuard interface in RouterOS.
     - Assign an IP address to the WireGuard interface (e.g., `192.168.99.1/24`).
  3. **Generate Keys**:
     - Generate a private and public key pair for the WireGuard server.
  4. **Configure Peers**:
     - Add peers for each device (e.g., laptop, phone, friends' devices).
     - Assign IPs to each peer (e.g., `192.168.99.2`, `192.168.99.3`, etc.).
  5. **Firewall Rules**:
     - Allow incoming UDP traffic on the WireGuard port (default: `51820`).
     - Ensure proper routing for WireGuard traffic to access the LAN or internet.
  6. **Test Connectivity**:
     - Test from external devices to ensure the VPN is working.

---

## 4. Home Server Setup

### 4.1 Select Operating System
- **Options**:
  - Proxmox VE: Dedicated virtualization OS.
  - Fedora/Arch with KVM: General-purpose OS with virtualization tools.
  - Other GUI-based solutions: VMware ESXi, XCP-ng, or Ubuntu Server with Cockpit.
- **Next Steps**:
  - Evaluate based on ease of use, GUI availability, and resource requirements.

### 4.2 Configure Virtual Machines
- **Objective**: Set up VMs for specific tasks.
- **Steps**:
  1. Install and configure the hypervisor.
  2. Create VMs for:
     - Private cloud.
     - Torrent client.
     - Other services.
  3. Register VMs with Azure Arc for management.

### 4.3 Set Up Containers
- **Objective**: Host services using Docker or Kubernetes.
- **Steps**:
  1. Install Docker or Kubernetes.
  2. Deploy containers for:
     - File sharing.
     - Media servers.
     - Other applications.
  3. Set up Kubernetes on VMs and integrate with Azure Arc.

---

## 5. File Sharing

### 5.1 Compare Solutions
- **Options**:
  - TrueNAS: Robust NAS solution with granular permissions.
  - Samba: Lightweight SMB sharing.
  - Nextcloud: Private cloud with advanced sharing options.
- **Next Steps**:
  - Test compatibility with older TVs, Android, Windows, and Linux.
  - Configure folders: Video, ISOs, torrent, tools, temp, and general share.

---

## 6. Testing and Validation
- **Objective**: Ensure everything works as expected.
- **Steps**:
  1. Test traffic forwarding and domain configuration.
  2. Verify VPN connectivity.
  3. Test all hosted services and file shares.
  4. Validate CI/CD pipelines and Azure Arc integration.

---

## 7. Documentation
- **Objective**: Maintain detailed records of the setup.
- **Steps**:
  1. Document all configurations (e.g., IP addresses, firewall rules).
  2. Update the `planning.md` file with any changes.

---

## 8. Integration with Work Environment

### 8.1 Hosting GitLab
- **Objective**: Host GitLab CE for CI/CD pipelines.
- **Steps**:
  1. Set up GitLab CE in a container or VM.
  2. Configure GitLab Runners for CI/CD pipelines.

### 8.2 Setting Up CI/CD Agents
- **Objective**: Run CI/CD pipelines using home lab resources.
- **Steps**:
  1. Install and configure CI/CD agents for:
     - GitLab Runner.
     - GitHub Actions self-hosted runners.
     - Azure DevOps agent.
  2. Configure all agents on the same VM if possible.
  3. Test CI/CD pipelines to ensure proper functionality.

### 8.3 Azure Integration
- **Objective**: Integrate the home lab with Azure for DevOps and cloud management.
- **Steps**:
  1. Register the home lab server and VMs with Azure Arc.
  2. Configure Azure services for:
     - Monitoring and management.
     - Deployment pipelines.
  3. Set up Kubernetes on VMs and integrate with Azure Arc.
  4. Test integration to ensure seamless operation between the home lab and Azure.

---

## 9. Testing and Validation
- Test traffic forwarding and domain configuration.
- Verify WireGuard connectivity.
- Test file sharing and hosted services.
- Validate CI/CD pipelines and Azure Arc integration.