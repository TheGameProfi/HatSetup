# Kavita

## Description
Kavita is a fast, feature rich, cross-platform reading server. Built with a focus for being a full solution for all your reading needs. Set up your own server and share your reading collection with your friends and family!

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
