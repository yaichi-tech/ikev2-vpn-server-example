# VPN Server

[日本語](README.ja.md)

IKEv2 VPN server using Docker. You can connect using your OS's built-in VPN functionality.

## Server Setup

Open the following ports on the server firewall:

- `500/udp` - IKE (Internet Key Exchange)
- `4500/udp` - IPsec NAT-Traversal

## Client Setup

### Windows

Windows 8, 10, and 11+ users can automatically import IKEv2 configuration.

1. Transfer the `.p12` file from the mounted `ikev2-vpn-data/` directory to your PC
2. Right-click on [ikev2_config_import.cmd](https://github.com/hwdsl2/vpn-extras/releases/latest/download/ikev2_config_import.cmd) and save to the same folder as the `.p12` file
3. Right-click on the saved script → Properties → Click "Unblock" at the bottom → OK
4. Right-click on the saved script → Select "Run as administrator" and follow the prompts

**Script Input Fields:**
| Field | Value |
|-------|-------|
| VPN client name | `VPN_CLIENT_NAME` in compose.yml |
| VPN server address | `VPN_DNS_NAME` in compose.yml |
| IKEv2 connection name | Any name is OK. Press Enter for default: "IKEv2 VPN {VPN_DNS_NAME}" |

**To connect to the VPN:**
Click on the network icon in your system tray → Select the new VPN entry → Click "Connect"

- Video: https://ko-fi.com/post/IKEv2-Auto-Import-Configuration-on-Windows-8-10-a-K3K1DQCHW

### Mac

Follow the documentation to open the `.mobileconfig` file, which will automatically add the VPN configuration.

The `.mobileconfig` file is located in the mounted `ikev2-vpn-data/` directory.

- Documentation: https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/docs/ikev2-howto.md#os-x-macos
- Video: https://ko-fi.com/post/IKEv2-Auto-Import-Configuration-on-Windows-8-10-a-K3K1DQCHW

## Verification

To verify the VPN connection is working correctly:

1. Visit https://www.cman.jp/network/support/go_access.cgi
2. Check your IP address
3. If it matches the server's IP address, the VPN is working as expected
