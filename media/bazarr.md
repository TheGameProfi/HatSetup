# Bazarr

## Description

Bazarr is an automated subtitle manager that works alongside tools like Sonarr and Radarr to download and manage subtitles for your TV shows and movies. It integrates with multiple subtitle providers, ensuring your media library always has the subtitles you need.

Key Features:
- Automatically downloads subtitles for TV shows and movies.
- Integrates seamlessly with Sonarr, Radarr, and Plex.
- Supports multiple subtitle providers, including OpenSubtitles, Addic7ed, and more.
- Customizable language and quality settings for subtitles.
- Monitors your library to ensure subtitles are always up to date.

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
