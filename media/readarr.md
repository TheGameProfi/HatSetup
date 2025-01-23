# Readarr

Readarr is currently in beta testing and is generally still in a work in progress. Features may be broken, incomplete, or cause spontaneous combustion

## Description
Readarr is an ebook and audiobook collection manager for Usenet and BitTorrent users. It can monitor multiple RSS feeds for new books from your favorite authors and will grab, sort, and rename them. Note that only one type of a given book is supported. If you want both an audiobook and ebook of a given book you will need multiple instances.

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