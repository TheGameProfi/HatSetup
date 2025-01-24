# SABnzbd

## Description

SABnzbd is a popular, open-source Usenet binary newsreader that automates the process of downloading, unpacking, and sorting files from Usenet newsgroups. With an easy-to-use web interface and powerful automation features, it simplifies Usenet downloading for users of all experience levels.

Key Features:
- Fully automated download and extraction process.
- Supports NZB files and integrates with popular automation tools (Sonarr, Radarr, etc.).
- Built-in post-processing features for unpacking, repairing, and categorizing downloaded content.
- Supports SSL, and configurable Usenet provider settings for optimal performance.
- Web-based interface with customizable themes and mobile-friendly access.


## Docker-Compose Setup

<table>
<tr>
<td>

```yaml
services:
    sabnzbd:
        image: lscr.io/linuxserver/sabnzbd
        container_name: sabnzbd
        volumes:
        - ./config/sabnzbd:/config
        - /downloads:/downloads
        restart: unless-stopped
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
        healthcheck:
            test: ping -c 1 1.1.1.1
            interval: 60s
            retries: 3
            start_period: 10s
            timeout: 10s
        depends_on:
            gluetun:
                condition: service_healthy
                restart: True
```
</td>
<td>
The Network Mode is set to the Gluetun Service (same Compose file), it routes all the Trafic trough Gluetun. <br />
The Healtcheck visualize if the Container is healthy connected to the VPN.
</td>
</tr>
</table>