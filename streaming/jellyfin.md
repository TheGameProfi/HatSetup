# Jellyfin

## Description
Jellyfin is a free and open-source media server that lets you manage, stream, and enjoy your media library across multiple devices. Whether it’s movies, TV shows, music, or photos, Jellyfin provides a self-hosted solution with full control over your content.

Key Features:
- No stings attached, no ads, and no Premium Versions.
- Stream movies, TV shows, music, and photos to any device.
- Fully self-hosted and open-source with no subscription fees.
- Multi-user support with custom permissions and profiles.
- Integration with popular clients on web, mobile, smart TVs, and more.
- Transcoding support for smooth playback on various devices.
- Plugins and customizations to extend functionality.

## Docker-Compose Setup

```yaml
services:
  jellyfin:
    image: jellyfin/jellyfin
    container_name: jellyfin
    environment:
      - PUID=1001
      - PGID=1001
    group_add:
      - 44 # Video Group for Encoding
      - 1001
    networks: 
      - media
    volumes:
      - ./config:/config
      - ./cache:/cache
      - /media/series:/media/series
      - /media/movies:/media/movies
    restart: 'unless-stopped'
    devices:
      - /dev/dri/renderD128:/dev/dri/renderD128
    ports:
      - 8096:8096
      - 8920:8920
      - 1900:1900
      - 7359:7359
```