# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Docker Compose configuration repository for setting up a comprehensive media server stack centered around Plex. It provides two compose templates:

- **basic-compose.yaml**: Core services (Plex, Radarr, Sonarr, Prowlarr, Overseerr, qBittorrent)
- **advanced-compose.yml**: Extended stack with 30+ additional services (Tdarr, Tautulli, Bazarr, Lidarr, Recyclarr, Backrest, etc.)

This is not application code—it's infrastructure configuration meant to be forked and customized.

## Commands

```bash
# Validate compose file syntax
docker compose -f docker-compose.yaml config

# Start the stack
docker compose up -d

# Stop the stack
docker compose down

# View logs for a specific service
docker compose logs -f <service-name>

# Restart a specific service
docker compose restart <service-name>

# Pull latest images and recreate
docker compose pull && docker compose up -d
```

## Environment Variables

Required variables that must be set (via `.env` file or Portainer):

| Variable | Example | Purpose |
|----------|---------|---------|
| `PUID` | `99` | User ID for container permissions |
| `GUID` | `101` | Group ID for container permissions |
| `TZ` | `Europe/Dublin` | Timezone |
| `BASE_PATH` | `/mnt/truenas/config` | Config directory for all services (bind mounts) |
| `DOCKER_PATH` | `/mnt/truenas/docker` | Persistent volumes for services (generated files, cache, etc.) |
| `MEDIA_SHARE` | `/mnt/truenas` | Root media storage path |
| `PLEX_CLAIM` | (from plex.tv/claim) | Plex server claim token |

Advanced stack may require additional variables: `PLEX_URL`, `PLEX_TOKEN`, `SERVER_IP`, `SONARR_KEY`, `RADARR_KEY`, `MEMBARR_TOKEN`.

## Architecture Patterns

### Volume Mounting Strategy
All *arr apps mount the entire `MEDIA_SHARE` to `/share` to enable hardlinking:
```yaml
volumes:
  - ${MEDIA_SHARE}:/share  # Enables hardlinks across downloads/media
```

Expected folder structure under `MEDIA_SHARE` (TrueNAS NFS mounts):
```
/mnt/truenas/           # MEDIA_SHARE
├── config/             # BASE_PATH - container configs
├── docker/             # DOCKER_PATH - persistent volumes
├── downloads/          # Torrent/Usenet downloads
├── movies/             # Movie library
├── tv/                 # TV shows library
├── music/              # Music library
└── xxx/                # Adult content library
```

### Service Conventions
- All services use LinuxServer.io images (`lscr.io/linuxserver/*`) where available
- Restart policy: `unless-stopped` for all services
- Config volumes: `${BASE_PATH}/<service>/config:/config`
- Persistent data (cache, generated files): `${DOCKER_PATH}/<service>/`
- Plex uses `network_mode: host`; other services use bridge networking
- Hardware transcoding: `/dev/dri:/dev/dri` device mapping for Intel QuickSync

### Adding New Services
When adding services, follow these patterns:
1. Use LinuxServer.io images if available
2. Include `PUID`, `PGID`, `TZ` environment variables
3. Mount config to `${BASE_PATH}/<service>/config:/config`
4. Mount persistent data (cache, generated) to `${DOCKER_PATH}/<service>/`
5. Mount media share as `/share` if the service needs media access
6. Use `restart: unless-stopped`

## Known Issues

### Gluetun breaks Docker image pulls
Gluetun uses `NET_ADMIN` + `cap_add` which modifies iptables rules on the host. This causes Docker to lose connectivity to container registries (ghcr.io, lscr.io, Docker Hub CDN). The issue persists even after stopping Gluetun.

**Workaround — always stop Gluetun before pulling images:**
```bash
docker stop gluetun qbittorrent
docker compose -f advanced-compose.yml pull
docker compose -f advanced-compose.yml up -d
```

If pulls still fail after stopping Gluetun, restart the Docker daemon:
```bash
sudo systemctl restart docker
docker compose -f advanced-compose.yml up -d
```

### Authelia pinned to v4.37
Authelia v4.38+ requires HTTPS for `authelia_url` in session cookies. Since this homelab uses HTTP internally with `.homelab` domains (no TLS), Authelia is pinned to `authelia/authelia:4.37` which supports the legacy `domain` config without HTTPS.

### Byparr zombie processes
Byparr spawns Camoufox/Firefox child processes that can accumulate as zombies. The `init: true` flag is set in compose to use tini as PID 1 and reap them automatically. Do not remove this flag.

### Kometa scheduled at 3 AM
Kometa (`KOMETA_TIME=03:00`) runs daily at 3 AM to avoid IO contention with Plex streaming. Do not set `KOMETA_RUN=true` in production — it triggers an immediate run on container start, which can cause buffering for active Plex streams.

## Backup Strategy

Backrest (restic web UI) backs up all service configs to TrueNAS:

- **Source 1:** `/mnt/truenas/config/` — all NFS-hosted service configs (`/sources/truenas-config` inside container)
- **Source 2:** `/opt/docker-configs/` — local SQLite DBs for *arr apps, Stash (`/sources/local-configs` inside container)
- **Destination:** `/mnt/truenas/backup-appdata/` — 2TB backup pool on TrueNAS (`/repos/truenas-backups` inside container)
- **Schedule:** Daily at 2 AM, prune weekly
- **Retention:** 7 daily, 4 weekly, 6 monthly
- **Management:** Web UI at https://backups.homelab

## External References

- [Trash Guides](https://trash-guides.info/) - Quality profiles and hardlink configuration
- [Hardlinks and Instant Moves](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) - Storage architecture guide
