# Radarr

## Description
Radarr is a movie collection manager for Usenet and BitTorrent users. It can monitor multiple RSS feeds for new movies and will interface with clients and indexers to grab, sort, and rename them. It can also be configured to automatically upgrade the quality of existing files in the library when a better quality format becomes available. Note that only one type of a given movie is supported. If you want both a 4k version and 1080p version of a given movie you will need multiple instances.

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