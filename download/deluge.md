# Deluge

## Description

Deluge is a lightweight, open-source BitTorrent client designed to be simple yet powerful. It offers a rich feature set while remaining highly extensible through plugins, making it a great choice for both casual users and advanced torrent management.

Key Features:
- Lightweight and responsive interface for efficient torrent management.
- Fully customizable with a variety of plugins to extend functionality.
- Supports encryption, DHT, PEX, and other popular BitTorrent protocols.
- Web-based control interface for managing torrents remotely.
- Comprehensive settings for bandwidth management, scheduling, and more.

## Docker-Compose Setup

```yaml
services:
  deluge:
    image: lscr.io/linuxserver/deluge:latest
    container_name: deluge
    environment:
      - PUID=1001
      - PGID=1001
      - TZ=Etc/UTC
      - DELUGE_LOGLEVEL=error #optional
    volumes:
      - ./config:/config
      - ./downloads:/downloads
    ports:
      - 8112:8112
      - 6881:6881
      - 6881:6881/udp
      - 58846:58846 #optional
    restart: unless-stopped
```