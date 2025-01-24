# Beets

## Documentation

Beets is a powerful, open-source music library manager designed to help you organize and manage your music collection. It provides automatic metadata retrieval, file renaming, and support for a wide variety of audio formats, making it easier to maintain a tidy and well-organized music library.

Key Features:
- Automatically organizes music files by artist, album, and track.
- Retrieves metadata (such as album art, genre, year, etc.) from multiple online sources.
- Supports various audio formats, including MP3, FLAC, and others.
- Flexible file renaming options to match your preferred naming scheme.
- Powerful plugin system to extend functionality (e.g., Last.fm, YouTube, etc.).


## Docker-Compose Setup

```yaml
---
services:
  beets:
    image: lscr.io/linuxserver/beets:latest
    container_name: beets
    environment:
      - PUID=1001
      - PGID=1001
      - TZ=Etc/UTC
    volumes:
      - ./config:/config
      - ./music:/music
      - ./ingest:/downloads
    ports:
      - 8337:8337
    restart: unless-stopped
```