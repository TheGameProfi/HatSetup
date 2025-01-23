# Jackett

## Description
Jackett works as a proxy server: it translates queries from apps (Sonarr, Radarr, SickRage, CouchPotato, Mylar3, Lidarr, DuckieTV, qBittorrent, Nefarious, NZBHydra2 etc.) into tracker-site-specific http queries, parses the html or json response, and then sends results back to the requesting software. This allows for getting recent uploads (like RSS) and performing searches. Jackett is a single repository of maintained indexer scraping & translation logic - removing the burden from other apps.

## Docker-Compose Setup

```yaml
    services:
        jackett:
            image: lscr.io/linuxserver/jackett:latest
            container_name: jackett
            environment:
            - PUID=1001
            - PGID=1001
            - TZ=Europa/Berlin
            - AUTO_UPDATE=true
            volumes:
            - ./config/jackett:/config
            - /downloads:/downloads
            ports:
            - 9117:9117
            networks:
            - media
            restart: unless-stopped
            extra_hosts:
            - "host.docker.internal:host-gateway"
```