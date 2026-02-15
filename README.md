# SDN Controller for MikroTik Devices

A C# .NET application that provides centralized management and control for MikroTik network devices running RouterOS. This SDN (Software-Defined Networking) controller offers a user-friendly interface for configuring and monitoring network infrastructure, including interfaces, wireless networks, routing, DHCP, DNS, and WireGuard VPN.

## Overview

This project aims to provide a centralized solution for managing MikroTik network infrastructure efficiently. By leveraging SDN principles, administrators can easily configure and monitor their devices through an intuitive desktop application. The controller communicates with MikroTik devices via the RouterOS REST API, enabling comprehensive network management from a single interface.

## Features

### Network Interface Management
- **LAN Interface Configuration**: View and configure LAN interfaces
- **Bridge Management**: Create, edit, and delete bridge interfaces
- **Bridge Port Control**: Manage bridge ports and their assignments

### Wireless Network Configuration
- **Security Profiles**: Create and manage wireless security profiles
- **Wireless Interfaces**: Configure, activate, and deactivate wireless interfaces
- **Profile Assignment**: Assign security profiles to wireless interfaces

### Routing Management
- **Static Routes**: View, create, edit, and delete static routes
- **Route Monitoring**: Monitor active routes and their status
- **Gateway Configuration**: Configure default gateways and route metrics

### IP Configuration
- **IP Address Management**: Assign and manage IP addresses on interfaces
- **DHCP Server**: Configure DHCP servers with custom address pools
- **DNS Configuration**: Manage DNS server settings

### WireGuard VPN
- **VPN Interface Management**: Create, edit, and delete WireGuard interfaces
- **Peer Configuration**: Manage WireGuard peers and their keys
- **Server/Client Setup**: Configure both VPN server and client setups
- **Key Management**: Generate and manage public/private key pairs

## Technology Stack

- **C# .NET Framework** - Core application development
- **Windows Forms** - Desktop GUI framework
- **RouterOS REST API** - MikroTik device communication
- **WireGuard** - Modern VPN protocol
- **Visual Studio** - Development environment

## Requirements

### Software Requirements
- **Visual Studio 2022** or later
- **.NET Framework 4.7.2** or higher
- **MikroTik RouterOS** v6.45 or higher (with REST API enabled)
- **WireGuard** (if using VPN features)

### Network Requirements
- Network connectivity to MikroTik devices
- RouterOS REST API enabled on target devices
- Administrative credentials for MikroTik devices

### Enabling REST API on MikroTik Devices

Connect to your MikroTik device and run:
```routeros
/ip service
set api-ssl disabled=no
set www-ssl disabled=no
```

Or enable via WinBox:
1. Open WinBox and connect to your device
2. Navigate to `IP → Services`
3. Enable `www-ssl` and `api-ssl`
4. Set appropriate ports (default: 443 for www-ssl)

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/WhyN0t101/SDN-Controller-MikroTik-Devices.git
   cd SDN-Controller-MikroTik-Devices
   ```

2. **Open in Visual Studio**
   - Open `LTI_RouterOS.sln` in Visual Studio 2022

3. **Restore NuGet Packages**
   - Right-click on solution → `Restore NuGet Packages`

4. **Build the Solution**
   - Press `Ctrl+Shift+B` or select `Build → Build Solution`

5. **Configure Connection**
   - Update connection settings for your MikroTik devices
   - Default protocol: HTTPS
   - Default port: 443

6. **Run the Application**
   - Press `F5` or click `Start`

## Configuration

### Device Connection

On first run, configure your MikroTik device connection:

1. **Device IP Address**: Enter the IP address of your MikroTik router
2. **Username**: Administrator username (default: `admin`)
3. **Password**: Administrator password
4. **Port**: REST API port (default: `443` for HTTPS)
5. **Protocol**: HTTP or HTTPS (HTTPS recommended)

### WireGuard Setup

To use WireGuard VPN features:

1. **Install WireGuard on MikroTik**
   ```routeros
   /interface wireguard
   add listen-port=13231 mtu=1420 name=wireguard1
   ```

2. **Configure via Controller**
   - Use the WireGuard tab in the application
   - Generate key pairs
   - Configure peers
   - Set allowed IPs

## Usage

### Main Interface

The application provides several tabs for different management tasks:

#### Interfaces Tab
- View all network interfaces
- Configure IP addresses
- Manage bridge interfaces
- Enable/disable interfaces

#### Wireless Tab
- Create security profiles
- Configure wireless interfaces
- Set SSID and channel
- Manage wireless clients

#### Routing Tab
- Add static routes
- Configure default gateway
- View routing table
- Set route preferences

#### DHCP Tab
- Create DHCP servers
- Define address pools
- Set lease times
- Configure DNS servers

#### WireGuard Tab
- Create VPN interfaces
- Add peers
- Generate keys
- Monitor VPN connections

### Common Operations

#### Creating a Bridge Interface

1. Navigate to Interfaces tab
2. Click "Create Bridge"
3. Enter bridge name
4. Add ports to bridge
5. Apply configuration

#### Setting Up WireGuard VPN

1. Go to WireGuard tab
2. Create new WireGuard interface
3. Generate keypair
4. Add peers with their public keys
5. Configure allowed IPs
6. Save and apply

## Troubleshooting

### Cannot Connect to Device

**Issue**: Controller can't connect to MikroTik device

**Solutions**:
- Verify device IP address is correct
- Check REST API is enabled on the device
- Verify firewall allows HTTPS/API connections
- Test connection with WinBox first
- Check credentials are correct

### SSL Certificate Errors

**Issue**: SSL/TLS certificate warnings

**Solutions**:
- Accept self-signed certificate (for development)
- Install proper SSL certificate on MikroTik
- Use HTTP instead (less secure, not recommended for production)

### WireGuard Not Working

**Issue**: WireGuard VPN not connecting

**Solutions**:
- Verify WireGuard is installed on MikroTik
- Check firewall rules allow WireGuard port (default: 13231/UDP)
- Verify public keys are correctly configured
- Check allowed IPs configuration
- Ensure routes are properly configured

### Configuration Changes Not Applied

**Issue**: Changes made in controller don't reflect on device

**Solutions**:
- Click "Apply" or "Save" after making changes
- Refresh the interface to see current state
- Check for error messages in the application
- Verify you have administrative privileges



## Security Considerations

- **HTTPS**: Always use HTTPS for production deployments
- **Credentials**: Never hardcode credentials in the application
- **API Access**: Restrict API access to trusted networks
- **WireGuard Keys**: Keep private keys secure and never share them
- **Firewall**: Configure firewalls to restrict access to management interfaces

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the GNU General Public License - see the [LICENSE.txt](LICENSE.txt) file for details.

---

**Note**: This is an educational project demonstrating SDN principles and MikroTik device management. For production environments, ensure proper security measures, testing, and backup procedures are in place before deployment.
