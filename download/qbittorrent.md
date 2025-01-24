# Qbittorrent & Flood


## Qbittorrent

### Description

qBittorrent is a fast, lightweight, and open-source BitTorrent client that provides a clean, user-friendly interface and a wealth of features. It supports all major torrenting protocols, including DHT, PEX, and encryption, while offering powerful options for managing torrents and trackers.

Key Features:
- Lightweight and easy-to-use interface.
- Full support for all major BitTorrent protocols, including DHT, PEX, and Magnet links.
- Built-in torrent search engine (with customizable indexers).
- Sequential downloading, bandwidth prioritization, and scheduling.
- Integrated media player for playback of downloaded content.
- Support for IP filtering, proxy settings, and encryption for privacy.

### Docker-Compose Setup

<table>
<tr>
<td>

```yaml
services:
    qbittorrent:
        image: lscr.io/linuxserver/qbittorrent
        container_name: qbittorrent
        restart: unless-stopped
        volumes:
            - ./config/qbittorrent:/config
            - /downloads:/downloads
        environment:
            - PUID=1001
            - PGID=1001
            - TZ=Europe/Berlin
```
</td>
<td>
</td>
</tr>
<tr>
<td>

```yaml
        network_mode: "service:gluetun"
        depends_on:
            gluetun:
                condition: service_healthy
                restart: True
        healthcheck:
            test: ping -c 1 1.1.1.1
            interval: 60s
            retries: 3
            start_period: 10s
            timeout: 10s
```
</td>
<td>
The Network Mode is set to the Gluetun Service (same Compose file), it routes all the Trafic trough Gluetun. <br />
The Healtcheck visualize if the Container is healthy connected to the VPN.
</td>
</tr>
</table>

    


## Flood

### Description

Flood (flood-ui) is a modern, web-based user interface for managing and interacting with torrent clients such as qBittorrent, Transmission, and Deluge. With an intuitive design and real-time updates, it provides an easy way to control and monitor your torrent downloads from any device with a web browser.

Key Features:
- Web-based UI for managing torrents remotely.
- Compatible with multiple torrent clients (qBittorrent, Transmission, Deluge, etc.).
- Real-time updates on torrent status, download speed, and more.
- Easy-to-navigate interface with detailed statistics and control options.
- Fully responsive and mobile-friendly.
- Authentication support for secure access.
- Open-source and lightweight, with an emphasis on simplicity.

### Docker-Compose Setup

<table>
<tr>
<td>

```yaml
services:
    food:
        image: jesec/flood
        container_name: flood
        user: 1001:1001
        environment:
            - PUID=1001
            - PGID=1001
            - TZ=Europe/Berlin
            - HOME=/config
        restart: unless-stopped
        command: --port 8081 --allowedpath /downloads
```
</td>
<td>
</td>
</tr>
<tr>
<td>

```yaml
        volumes:
            - ./config/flood:/config
            - /downloads:/downloads
```
</td>
<td>
Flood manages the Torrent Downloads for that reason it needs to have the same Filesystem as the Torrent Client.
</td>
</tr>
<tr>
<td>

```yaml
        networks:
            - media
        ports:
            - 8081:8081
```
</td>
<td>
Since Flood is only managing the Downloads it doesn't need to be connected to the VPN, and the Ports need to be Exposed directly.
</td>
</tr>
</table>
