# Readarr

Readarr is currently in beta testing and is generally still in a work in progress. Features may be broken, incomplete, or cause spontaneous combustion

## Description
Readarr is an automated eBook and audiobook manager designed to help you track, download, and organize your digital library. It integrates with popular download clients and indexers to simplify managing your reading collection.

Key Features:
- Automatically tracks and downloads eBooks and audiobooks.
- Supports multiple download clients, including Usenet and BitTorrent.
- Custom quality profiles for different formats (ePub, PDF, Mobi, etc.).
- Built-in support for public and private indexers.
- Organizes and renames books based on your preferences.

## Docker-Compose Setup

```yaml
services:
  readarr:
    image: lscr.io/linuxserver/readarr:develop
    container_name: readarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
    volumes:
      - ./config/readarr:/config
      - /media/media/books/readarr:/books #optional
      - /downloads:/downloads #optional
    ports:
      - 8787:8787
    restart: unless-stopped
    networks:
      - media
    extra_hosts:
      - "host.docker.internal:host-gateway"
```