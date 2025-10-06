# Upstream Planning

## 1. Coordinate with Landlord's IT
- **Objective**: Forward specific traffic from the landlord's SonicWall router to your MikroTik router.
- **Steps**:
  1. Request the landlord's IT to forward traffic to your router's IP address.
  2. Decide on traffic filtering:
     - Option 1: Forward all traffic for your domain `3ranger13.eu` to your router.
     - Option 2: Forward all traffic via WireGuard VPN (requires one UDP port to be forwarded).
  3. Provide the necessary details to the landlord's IT:
     - Your router's IP address.
     - The domain name or specific ports to forward.

## 2. Domain Configuration
- **Objective**: Configure `3ranger13.eu` to route traffic to your network.
- **Steps**:
  1. Update DNS records to point to the landlord's public IP address.
  2. Ensure traffic is forwarded to your MikroTik router.

## 3. Traffic Forwarding Plan
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