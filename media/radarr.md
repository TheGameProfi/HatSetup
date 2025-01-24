# Radarr

## Description
Radarr is a powerful movie collection manager that helps you automate the process of tracking, downloading, and organizing movies. It integrates seamlessly with popular download clients and indexers, making it easy to maintain and expand your movie library.

Key Features:
- Automatically tracks and downloads movies.
- Supports Usenet and BitTorrent download clients.
- Customizable quality profiles to manage resolution and formats.
- Built-in support for hundreds of public and private indexers.
- Organizes and renames movies based on your preferred structure.

## Docker-Compose Setup

```yaml
services:
    radarr:
        image: lscr.io/linuxserver/radarr
        container_name: radarr
        networks:
        - media
        environment:
        - PUID=1001
        - PGID=1001
        - TZ=Europe/Berlin
        extra_hosts:
        - "host.docker.internal:host-gateway"
        volumes:
        - /media/movies:/media/
        - ./config/radarr:/config
        - /downloads/:/downloads
        ports:
        - 7878:7878
        restart: unless-stopped
```