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

---

## 3. Network Topology Plan
- **Core Components**:
  - Router: High-performance router with advanced features (e.g., VLANs, QoS, firewall).
  - Switches: Managed switches for better traffic control.
  - Access Points: Multiple Wi-Fi access points for better coverage.
- **Segmentation**:
  - VLANs to separate traffic (e.g., IoT devices, guest network, lab network).
  - DMZ for public-facing services.
- **IP Addressing**:
  - Consistent IP addressing scheme (e.g., 192.168.x.x or 10.x.x.x).
  - Static IPs for critical devices.

---

## 4. Home Lab Setup
- **Hardware**:
  - Dedicated server or repurposed old hardware.
  - NAS for centralized storage.
  - Virtualization tools: Proxmox, VMware ESXi, or Hyper-V.
- **Software**:
  - Containerization: Docker or Kubernetes for running services.
  - Monitoring: Grafana, Prometheus, or Zabbix.
  - Automation: Ansible, Terraform, or similar tools.
- **Services**:
  - DNS: Local DNS server (e.g., Pi-hole, Unbound).
  - VPN: Secure remote access (e.g., WireGuard, OpenVPN).
  - Reverse Proxy: Managing web services (e.g., Nginx, Traefik).

---

## 5. Security Best Practices
- Robust firewall (e.g., pfSense, OPNsense).
- Regular updates for all devices and software.
- Reliable backup strategy.
- Strong passwords and multi-factor authentication (MFA).

---

## 6. Tools for Planning and Documentation
- **Network Diagram Tools**: draw.io, Lucidchart, or Visio.
- **Documentation**: Maintain detailed records of the setup (e.g., IP addresses, configurations).

---

## 7. Budget and Timeline
- **Budget**: Determine spending limits for hardware and software.
- **Timeline**: Break the project into phases (e.g., network upgrade, lab setup).

---

## 8. Testing and Iteration
- Start small and test each component before scaling up.
- Monitor performance and make adjustments as needed.