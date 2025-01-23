# Qbittorrent & Flood


## Qbittorrent

### Description

qBittorrent is a bittorrent client that connects to various Seeders and download the Files. <br />
When the Download is finished the Files are getting "seeded", meaing that the Files are getting shared with other Users all over the World who are trying to download the same Files.

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

Flood is a Service that manages the Torrent Downloads. It's an more modern UI for various Torrent Clients.

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
