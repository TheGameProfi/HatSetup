# Bazarr

## Description

Bazarr is a companion application to Sonarr and Radarr. It manages and downloads subtitles based on your requirements. You define your preferences by TV show or movie and Bazarr takes care of everything for you.

## Docker-Compose Setup

```yaml
services:
    bazarr:
        image: lscr.io/linuxserver/bazarr:latest
        container_name: bazarr
        networks:
        - media
        environment:
        - PUID=1001
        - PGID=1001
        - TZ=Europe/Berlin
        extra_hosts:
        - "host.docker.internal:host-gateway"
        volumes:
        - /media/movies:/movies/
        - /media/series:/series/
        - ./config/bazarr:/config
        ports:
        - 6767:6767
        restart: unless-stopped
```
