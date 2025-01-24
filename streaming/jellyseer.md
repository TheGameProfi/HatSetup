# Jellyseer

## Description
Jellyseer is a lightweight, open-source client for managing and interacting with Jellyfin media servers. It provides an easy-to-use interface for controlling playback, managing libraries, and monitoring server status from a web-based dashboard.

Key Features:
- Control Jellyfin servers remotely from any device with a web browser.
- Manage libraries, playlists, and media content with ease.
- Monitor server status, including media playback and system performance.
- Fully open-source and lightweight with no server installation required.
- Cross-platform compatibility (works on any device with a browser).

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