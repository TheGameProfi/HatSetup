# Jackett

## Description
Jackett is an API support service that acts as a proxy for various BitTorrent and Usenet indexers, allowing them to work seamlessly with automation tools like Sonarr, Radarr, and Lidarr. It provides a unified interface for accessing and searching indexers, simplifying media automation.

Key Features:
- Acts as a bridge between automation tools and indexers.
- Supports over 500 public and private BitTorrent and Usenet indexers.
- Provides a unified API for easy integration with tools like Sonarr, Radarr, Lidarr, and Prowlarr.
- Customizable search filters for fine-tuned results.

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