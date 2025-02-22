# Home Services Infrastructure

This repository contains the configuration for various self-hosted services running on my home server.

## Services Overview

### Media Management
- **Sonarr** - TV Series Management
  - Port: 8989
  - URL: http://localhost:8989
  - Data Location: `/data/tv`

- **qBittorrent** - Download Client
  - Port: 9091 (WebUI)
  - URL: http://localhost:9091
  - Download Location: `/data/downloads`
  - VPN: Enabled with WireGuard
  - LAN Access: Enabled on port 9091

- **Prowlarr** - Indexer Management
  - Port: 9696
  - URL: http://localhost:9696

### Photo Management
- **Immich** - Photo Management & Backup
  - URL: https://photos.relaymate.com
  - Server Port: 2283
  - Components:
    - Server
    - Machine Learning
    - PostgreSQL Database
    - Redis Cache
  - Media Location: `/data/photos`
  - Database Location: `/data/db/immich`

### Home Automation
- **Home Assistant** - Home Automation Platform
  - Network: Host Network
  - Configuration: `/config/homeassistant`
  - Features:
    - Automations
    - Scenes
    - Scripts
    - Custom Blueprints

### Networking
- **Caddy** - Reverse Proxy & DDNS
  - Network: Host Network
  - Features:
    - Automatic HTTPS
    - Cloudflare DDNS Integration
    - SSL Certificate Management

## Directory Structure
```
.
├── compose.yaml          # Main compose file
├── immich/
│   └── compose.yaml      # Immich specific compose
├── config/
│   ├── caddy/           # Caddy configuration
│   ├── homeassistant/   # Home Assistant configuration
│   ├── prowlarr/        # Prowlarr configuration
│   ├── qbittorrent/     # qBittorrent configuration
│   └── sonarr/          # Sonarr configuration
└── .env                 # Environment configuration
```

## Data Locations
All media and service data is stored under `/data/`:
- `/data/tv` - TV Series
- `/data/downloads` - Temporary download location
- `/data/photos` - Photo library
- `/data/db/immich` - Immich database

## Environment Configuration
Key environment variables are managed in `.env` file:
- Media paths
- Domain configuration
- Service credentials
- VPN settings

## Security Notes
- VPN is enabled for qBittorrent with WireGuard
- Sensitive data and credentials are excluded from git
- All services run with PUID/PGID 1000
- Cloudflare integration for secure access

## Backup Considerations
The following locations should be backed up:
- `/config/*` - Service configurations
- `/data/photos` - Photo library
- `/data/db/immich` - Immich database
- `.env` file - Environment configuration

## Getting Started
1. Clone this repository
2. Copy `.env.example` to `.env` and configure variables
3. Create required directories under `/data`
4. Run `docker compose up -d`

## Network Requirements
- Port 80/443 for Caddy HTTPS
- Port 9091 for qBittorrent WebUI
- Port 8989 for Sonarr
- Port 9696 for Prowlarr
- Port 2283 for Immich 