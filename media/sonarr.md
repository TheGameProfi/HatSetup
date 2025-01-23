# Sonarr

## Description

Sonarr is a PVR for Usenet and BitTorrent users. It can monitor multiple RSS feeds for new episodes of your favorite shows and will grab, sort and rename them. It can also be configured to automatically upgrade the quality of files already downloaded when a better quality format becomes available.


## Docker-Compose Setup

```yaml
services:
    sonarr:
        image: lscr.io/linuxserver/sonarr
        container_name: sonarr
        networks:
        - media
        environment:
        - PUID=1001
        - PGID=1001
        - TZ=Europe/Berlin
        extra_hosts:
        - "host.docker.internal:host-gateway"
        volumes:
        - /media/series:/media/
        - ./config/sonarr:/config
        - /downloads/:/downloads
        ports:
        - 8989:8989
        restart: unless-stopped
```