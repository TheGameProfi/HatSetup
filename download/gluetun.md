# Gluetun

## Overview

Best Practice is to keep all the Hat touching the Outside World behind a VPN.
With Gluetun we can create a VPN Tunnel which the services can use to connect to the Internet, also it has a build-in Proxy to allow us to connect to the Services.

The other container need to be Setup with the Network mode to the Gluetun Container with ```network_mode: service:gluetun``` or ```network_mode: container:gluetun``` or as CLI ```--network=container:gluetun```... <br />
Since the Network-Mode is a Override the Port need to be Exposed from the Gluetun Container and not the other Containers.

## Description

Gluetun is an open-source VPN client that allows you to securely route your network traffic through a VPN server, providing enhanced privacy and anonymity. It can be easily integrated with Docker and is designed to work seamlessly with other services like qBittorrent, Plex, and more, making it ideal for securing your internet connection while running various applications.

Key Features:
- Supports multiple VPN providers (e.g., Mullvad, NordVPN, PIA, etc.).
- Easy-to-setup and configure with Docker.
- DNS and IP leak protection.
- Provides a simple web interface for monitoring VPN connections.
- Customizable firewall rules for better network security.
- Supports both OpenVPN and WireGuard protocols.

## Docker Compose Setup

<table>
<tr>
<td>

```yaml
gluetun:
    image: qmcgaw/gluetun
    container_name: gluetun
```
</td>
<td>
</td>
</tr>
<tr>
<td>

```yaml
    cap_add:
        - NET_ADMIN
    devices:
        - /dev/net/tun:/dev/net/tun
```
</td>
<td>
Needed Options to allow Gluetun to create a VPN Tunnel
</td>
</tr>
<tr>
<td>

```yaml
    environment:
        - VPN_SERVICE_PROVIDER=mullvad # For Different VPN Provider follow https://github.com/qdm12/gluetun-wiki/tree/main/setup/providers
        - VPN_TYPE=wireguard
        - WIREGUARD_PRIVATE_KEY=PRIVATE_KEY # Private Key for Wireguard
        - WIREGUARD_ADDRESSES=ADDRESSES # Address from Wireguard Config (ipv6 needs to be configured in Docker)
        - SERVER_COUNTRIES=Sweden,Netherlands
        - OWNED_ONLY=yes # Only use Servers owned by Mullvad
```
</td>
<td>

Detailed Instructions can be found in the [Gluetun Wiki](https://github.com/qdm12/gluetun-wiki)
</td>
</tr>
<tr>
<td>

```yaml
    networks:
        - media # Specifying Network for media Services
     # Device need for Tunnel Creation
    sysctls:
        - net.ipv6.conf.all.disable_ipv6=0 # Enable ipv6
    ports:
        - 8085:8085 # Sabnzbd Port
```
</td>
<td>
Since the Download Services are getting Routed trough Gluetun all the Ports need to be Exposed from the Gluetun Container
</td>
</tr>
<tr>
<td>

```yaml
    healthcheck:
        test: ping -c 1 1.1.1.1
        interval: 60s
        retries: 3
        start_period: 20s
        timeout: 10s
    volumes:
        - ./data:/gluetun
    restart: unless-stopped
```
</td>
<td>
Configuration of an Healthcheck to ensure the Vpn Connection is running and the other Services are getting Restarted if the VPN restarts.
Add Volumes and Restarts
</td>
</tr>
</table>
