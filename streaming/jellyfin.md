# Jellyfin

## Description
Jellyfin is a Free Software Media System that puts you in control of managing and streaming your media. It is an alternative to the proprietary Emby and Plex, to provide media from a dedicated server to end-user devices via multiple apps. There are no strings attached, no premium licenses or features, and no hidden agendas: just a team who want to build something better and work together to achieve it. We welcome anyone who is interested in joining us in our quest!

## Docker-Compose Setup

```yaml
services:
  jellyfin:
    image: jellyfin/jellyfin
    container_name: jellyfin
    environment:
      - PUID=1001
      - PGID=1001
    group_add:
      - 44 # Video Group for Encoding
      - 1001
    networks: 
      - media
    volumes:
      - ./config:/config
      - ./cache:/cache
      - /media/series:/media/series
      - /media/movies:/media/movies
    restart: 'unless-stopped'
    devices:
      - /dev/dri/renderD128:/dev/dri/renderD128
    ports:
      - 8096:8096
      - 8920:8920
      - 1900:1900
      - 7359:7359
```