# Prowlarr

## Description

Prowlarr is a powerful indexer manager for managing both Usenet and BitTorrent indexers. It acts as a centralized service for discovering and managing indexers, seamlessly integrating with popular download clients and automation tools like Sonarr, Radarr, and Lidarr.

Key Features:
- Supports both Usenet and BitTorrent indexers.
- Unified interface for managing indexers with easy configuration.
- Full API integration with automation tools.
- Scheduled updates and health monitoring for indexers.
- Built-in support for over 500 public and private indexers.

## Docker-Compose Setup

```yaml
services:
  prowlarr:
    image: lscr.io/linuxserver/prowlarr:latest
    container_name: prowlarr
    environment:
      - PUID=1001
      - PGID=1001
      - TZ=Etc/UTC
    volumes:
      - ./config:/config
    ports:
      - 9696:9696
    restart: unless-stopped
```