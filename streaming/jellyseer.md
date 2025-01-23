# Jellyseer

## Description
Jellyseerr is a free and open source software application for managing requests for your media library. It integrates with the media server of your choice: Jellyfin, Plex, and Emby. In addition, it integrates with your existing services, such as Sonarr, Radarr.

## Docker-Compose Setup

```yaml
services:
  jellyseerr:
    image: fallenbagel/jellyseerr:latest
    container_name: jellyseerr
    environment:
      - LOG_LEVEL=info
      - TZ=Europe/Berlin
      - PORT=5055 #optional
    ports:
      - 5055:5055
    networks:
      - media
    volumes:
      - ./config:/app/config
    restart: unless-stopped
```