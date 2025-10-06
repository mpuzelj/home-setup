# WireGuard Setup

## Decide on WireGuard Server Location
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

## Configure WireGuard
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

## MikroTik as WireGuard Server
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