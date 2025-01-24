# Kavita

## Description
Kavita is an open-source eBook and manga management system that allows you to organize, read, and enjoy your digital library. With a clean, user-friendly interface, Kavita supports a variety of formats and provides an easy-to-use platform for managing your collection from any device.

Key Features:
- Supports eBooks (EPUB, PDF, and MOBI) and manga (CBZ, CBR).
- Allows you to organize your library, track reading progress, and manage metadata.
- Provides a responsive and clean user interface for easy navigation.
Cross-platform support (Windows, macOS, Linux, Docker).
- Full-text search, tagging, and filtering options for your library.
- Built-in support for metadata scraping from various sources.
- Syncs reading progress across devices.

## Docker-Compose Setup

```yaml
services:
    kavita:
        image: jvmilazz0/kavita:latest
        environment:
        - PUID=1001
        - PGID=1001
        volumes:
        - /media/books:/books
        - ./config:/kavita/config
        ports:
        - "5000:5000"
        restart: unless-stopped
```
