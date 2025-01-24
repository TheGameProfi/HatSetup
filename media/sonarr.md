# Sonarr

## Description

Sonarr is an advanced PVR (Personal Video Recorder) for automatically managing and downloading TV series. It seamlessly integrates with your favorite download clients and indexers, providing an automated way to track, download, and organize your shows.

Key Features:
- Automatically tracks and downloads TV series.
- Supports multiple download clients like Usenet and BitTorrent.
- Advanced episode monitoring with custom quality profiles.
- Easy integration with indexers through built-in support for over 500 options.
- Renames and organizes episodes to match your preferred structure.
- Full API for integration with other tools and services.


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