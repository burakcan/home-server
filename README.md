# Home Services Infrastructure

This repository contains the configuration for various self-hosted services running on my home server.

## Services Overview

### Media Management
- **Sonarr** - TV Series Management
  - Port: 8989
  - URL: http://localhost:8989 or https://${SONARR_DOMAIN}
  - Data Location: `${TV_DIR}`

- **Radarr** - Movie Management
  - Port: 7878
  - URL: http://localhost:7878 or https://${RADARR_DOMAIN}
  - Data Location: `${MOVIES_DIR}`

- **qBittorrent** - Download Client
  - Port: 9091 (WebUI)
  - URL: http://localhost:9091 or https://${QBITTORRENT_DOMAIN}
  - Download Location: `${DOWNLOADS_DIR}`
  - VPN: Enabled with WireGuard
  - LAN Access: Enabled on port 9091

- **Prowlarr** - Indexer Management
  - Port: 9696
  - URL: http://localhost:9696

- **Byparr** - Captcha solving service
  - Port: 8191
  - Used by Prowlarr for handling captchas

### Media Streaming
- **Plex** - Media Server
  - Port: 32400
  - URL: http://localhost:32400 or https://${PLEX_DOMAIN}
  - Media Location: `${MEDIA_ROOT}`

- **Jellyfin** - Media Server
  - Port: 8096
  - URL: http://localhost:8096 or https://${JELLYFIN_DOMAIN}
  - Media Location: `${MEDIA_ROOT}`

### Photo Management
- **Immich** - Photo Management & Backup
  - Port: 2283
  - URL: https://${IMMICH_DOMAIN}
  - Components:
    - Server
    - Machine Learning
    - PostgreSQL Database
    - Redis Cache
  - Media Location: `${PHOTOS_DIR}`
  - Database Location: `${DB_DATA_LOCATION}`

### Home Automation
- **Home Assistant** - Home Automation Platform
  - Network: Host Network
  - URL: https://${HOMEASSISTANT_DOMAIN}
  - Configuration: `./config/homeassistant`

### Networking & UI
- **Caddy** - Reverse Proxy & DDNS
  - Network: Host Network
  - Features:
    - Automatic HTTPS
    - Cloudflare DDNS Integration
    - SSL Certificate Management

- **Homepage** - Dashboard for Services
  - Port: 3000
  - URL: http://localhost:3000 or https://${HOMEPAGE_DOMAIN}

## Directory Structure
```
.
├── compose.yaml          # Main compose file
├── immich/
│   └── compose.yaml      # Immich specific compose
├── config/
│   ├── caddy/            # Caddy configuration
│   ├── homeassistant/    # Home Assistant configuration
│   ├── homepage/         # Homepage configuration
│   ├── plex/             # Plex configuration
│   ├── jellyfin/         # Jellyfin configuration
│   ├── prowlarr/         # Prowlarr configuration
│   ├── qbittorrent/      # qBittorrent configuration
│   ├── radarr/           # Radarr configuration
│   └── sonarr/           # Sonarr configuration
└── .env                  # Environment configuration
```

## Environment Configuration
Key environment variables are managed in `.env` file. Copy `.env.example` to `.env` and configure:
- Media paths
- Domain configuration
- Service credentials
- VPN settings

## Security Notes
- VPN is enabled for qBittorrent with WireGuard
- Sensitive data and credentials should be added to `.env` (excluded from git)
- All services run with configured PUID/PGID
- Cloudflare integration for secure access

## Backup Considerations
The following locations should be backed up:
- `./config/*` - Service configurations
- `${PHOTOS_DIR}` - Photo library
- `${DB_DATA_LOCATION}` - Immich database
- `.env` file - Environment configuration

## Getting Started
1. Clone this repository
2. Copy `.env.example` to `.env` and configure variables
3. Create required directories specified in `.env`
4. Run `docker compose up -d`

## Network Requirements
- Port 80/443 for Caddy HTTPS
- Port 9091 for qBittorrent WebUI
- Port 8989 for Sonarr
- Port 7878 for Radarr
- Port 9696 for Prowlarr
- Port 32400 for Plex
- Port 3000 for Homepage
- Port 8096 for Jellyfin
- Port 2283 for Immich 