# <img src="/ultimate_plex_stack_transparent_bg.png" width="300px" alt="The Ultimate Plex Stack"></img>

> **Fork Notice:** This repository is a fork of the original [ultimate-plex-stack](https://github.com/DonMcD/ultimate-plex-stack). The goal of this fork is to modernize the stack, replacing deprecated tools with current alternatives and maintaining best practices for 2025/2026.

Welcome to my stack repository! This repository showcases my docker compose setup for managing various media-related services using Docker containers. The compose file is meant to be modified to each user's liking as I know, not everyone has the same requirements.

Currently you can choose from the **Basic** or the **Advanced** compose.

---

## Tool Analysis (2025/2026)

### Status Legend

| Status | Meaning |
|--------|---------|
| :white_check_mark: | Active and recommended |
| :warning: | Functional, but with caveats |
| :x: | Deprecated - replace |
| :arrows_counterclockwise: | Migration recommended |

### Detailed Analysis

| Tool | Status | Analysis | Recommendation |
|------|--------|----------|----------------|
| **AdGuard Home** | :white_check_mark: | Network-wide DNS with ad blocking. Lightweight, easy to configure. Supports DNS-over-HTTPS/TLS. | Keep. Alternatives: [Pi-hole](https://pi-hole.net/), [Blocky](https://github.com/0xERR0R/blocky). |
| **Traefik** | :white_check_mark: | Modern reverse proxy with automatic SSL and Docker integration. Cloud-native design. | Keep. Alternatives: [Nginx Proxy Manager](https://nginxproxymanager.com/), [Caddy](https://caddyserver.com/). |
| **Plex** | :white_check_mark: | Remains the most polished and user-friendly media server. Extensive device support. Plex Pass optional for advanced features. | Keep. Alternatives: [Jellyfin](https://jellyfin.org/) (open-source, free) or [Emby](https://emby.media/). |
| **Radarr** | :white_check_mark: | Actively maintained. Part of the Servarr ecosystem. | Keep. |
| **Sonarr** | :white_check_mark: | Actively maintained. Requires v4+. | Keep. |
| **Prowlarr** | :white_check_mark: | Actively maintained. Supports 500+ torrent trackers and 24+ Usenet indexers. | Keep. |
| **Readarr** | :x: | LinuxServer.io image deprecated. No amd64 support available. | **Disabled** - waiting for upstream fix. |
| **Lidarr** | :white_check_mark: | Actively maintained for music automation. | Keep. |
| **qBittorrent** | :white_check_mark: | Ranked #1 among torrent clients. Supports up to 10,000 torrents. | Keep. Alternatives: [Transmission](https://transmissionbt.com/) (lighter), [Deluge](https://deluge-torrent.org/) (more customizable via plugins). |
| **Overseerr** | :arrows_counterclockwise: | Being **deprecated** and merged with Jellyseerr into a new project called **Seerr**. | **Migrate to [Seerr](https://github.com/seerr-team/seerr)** - supports Plex, Jellyfin and Emby. |
| **Plex Meta Manager** | :x: | **DEPRECATED** in April 2024. Project renamed to Kometa. LinuxServer.io no longer supports the old image. | **Replace with [Kometa](https://github.com/Kometa-Team/Kometa)** (`kometateam/kometa`). |
| **Tdarr** | :warning: | Functional and powerful for distributed transcoding. Closed-source. | Keep. Open-source alternative: [Unmanic](https://github.com/Unmanic/unmanic). |
| **Tautulli** | :white_check_mark: | Remains the best monitoring tool for Plex. Some antivirus may generate false positives. | Keep. |
| **Bazarr** | :white_check_mark: | Actively maintained. Python 3.13+ support. Improved OpenSubtitles integration. | Keep. |
| **Autobrr** | :white_check_mark: | Actively maintained (Go 1.25+). Best option for IRC automation. | Keep. |
| **Flaresolverr** | :arrows_counterclockwise: | Cloudflare constantly updates its protections. FlareSolverr struggles to keep up. | **Consider migrating to [Byparr](https://github.com/ThePhaseless/Byparr)** - more modern drop-in replacement using Camoufox. |
| **Wizarr** | :white_check_mark: | Actively maintained (v2025.10.5+). Supports Plex, Jellyfin, Emby, Audiobookshelf, Romm, Komga and Kavita. | Keep. |
| **Dozzle** | :white_check_mark: | Lightweight and efficient for real-time logs. Supports Docker, Swarm, K8s, Podman. | Keep. For historical logs/search, consider [Loki + Grafana](https://grafana.com/oss/loki/). |
| **Plex Auto Languages** | :warning: | Original project (RemiRigal) may have been abandoned. Community forks (JourneyDocker, thesammykins) continue. Issues reported on TrueNAS Scale. | Use active fork: `journeyover/plex-auto-languages` or TypeScript rewrite by thesammykins. |
| **Unpackerr** | :white_check_mark: | Actively maintained. Supports RAR, ZIP, 7ZIP, TAR and more. Auto-detection of *arr apps. | Keep. |
| **Recyclarr** | :white_check_mark: | Actively maintained. TRaSH Guides updated in January 2026. Supports Radarr and Sonarr v4+. | Keep. |
| **Whisparr** | :white_check_mark: | Part of the Servarr ecosystem. Automated adult content management. Integrates with Prowlarr. | Keep. |
| **Stash** | :white_check_mark: | Adult media organizer with metadata scraping, tagging, web streaming. | Keep. |
| **Homepage** | :white_check_mark: | Modern, highly customizable dashboard. Supports widgets for all *arr apps. | Keep. |
| **MeTube** | :white_check_mark: | Web UI for yt-dlp supporting YouTube and 1000+ sites. Browser extensions available. | Keep. |
| **Forgejo** | :white_check_mark: | Community-driven Git service fork of Gitea. Lightweight, actively maintained, focused on sustainability. | Keep. Alternatives: [Gitea](https://gitea.io/), [GitLab](https://gitlab.com/). |
| **Gluetun** | :white_check_mark: | VPN client supporting 30+ providers. Routes container traffic through VPN tunnel via WireGuard/OpenVPN. | Keep. Essential for torrent privacy. |
| **Authelia** | :white_check_mark: | Open-source SSO and 2FA portal. Integrates with Traefik as forward-auth middleware. | Keep. Alternatives: [Authentik](https://goauthentik.io/). |
| **Vaultwarden** | :white_check_mark: | Lightweight Bitwarden server implementation in Rust. Full API compatibility. | Keep. |
| **Docker Socket Proxy** | :white_check_mark: | Secure proxy to Docker socket. Limits API access for containers that need Docker info. | Keep. Security best practice. |
| **WireGuard Easy** | :white_check_mark: | Simple WireGuard VPN server with web management UI. | Keep. |
| **Scrutiny** | :white_check_mark: | S.M.A.R.T. disk monitoring with web UI and alerting. | Keep. |
| **Gotify** | :white_check_mark: | Self-hosted push notification server with REST API and web client. | Keep. |
| **Maintainerr** | :white_check_mark: | Automated Plex library maintenance based on custom rules. | Keep. |
| **Speedtest Tracker** | :white_check_mark: | Automated internet speed tests with historical data and graphs. | Keep. |
| **IT-Tools** | :white_check_mark: | Collection of 80+ developer and networking tools in a web UI. | Keep. |
| **Mealie** | :white_check_mark: | Recipe management with meal planning, shopping lists, and URL import. | Keep. |
| **Actual Budget** | :white_check_mark: | Privacy-focused personal finance with envelope budgeting. Local-first, no cloud dependency. | Keep. |

---

## Priority Changes for Modernization

### :x: Mandatory Replacements

1. **Plex Meta Manager → Kometa**
   ```yaml
   # Before (deprecated)
   plex-meta-manager:
     image: meisnate12/plex-meta-manager

   # After
   kometa:
     image: kometateam/kometa
   ```

2. **Overseerr → Seerr**
   ```yaml
   # Before (will be deprecated)
   overseerr:
     image: lscr.io/linuxserver/overseerr:latest

   # After
   seerr:
     image: ghcr.io/seerr-team/seerr:develop
   ```

### :arrows_counterclockwise: Recommended Migrations

3. **Flaresolverr → Byparr** (if facing Cloudflare issues)
   ```yaml
   # More modern alternative
   byparr:
     image: ghcr.io/thephaseless/byparr:latest
   ```

---

## Overview

**Basic Compose** Includes:

- **Plex:** Media server for streaming movies and TV shows.
- **Radarr:** Movie management and automation.
- **Sonarr:** TV show management and automation.
- **Prowlarr:** Indexer manager for Radarr and Sonarr.
- **Seerr:** Request management and monitoring for Plex/Jellyfin/Emby.
- **qBittorrent:** BitTorrent client.

**Advanced Compose** Includes:

- **AdGuard Home:** Network-wide DNS with ad blocking.
- **Traefik:** Reverse proxy for friendly URLs and SSL.
- **Plex:** Media server for streaming movies and TV shows.
- **Radarr:** Movie management and automation.
- **Sonarr:** TV show management and automation.
- **Prowlarr:** Indexer manager for Radarr and Sonarr.
- **Seerr:** Request management for Plex/Jellyfin/Emby.
- **qBittorrent:** BitTorrent client.
- **Tdarr:** Pre-transcodes your media to decrease file sizes.
- **Tautulli:** Analytics and monitoring for Plex.
- **Bazarr:** Subtitle management for movies and TV shows.
- **Autobrr:** Used to grab torrents immediately as they are released.
- **Lidarr:** Used to grab music.
- **Byparr:** Used as a proxy server to bypass Cloudflare and DDoS-GUARD protection.
- **Dozzle:** Used to view the logs of any container.
- **Wizarr:** Used to create links that can be sent to users so they can be invited to your media server.
- **Kometa:** Used to create collections, overlays, playlists and much more! *(Formerly Plex Meta Manager)*
- **Recyclarr:** Used to sync the config of TRaSH Guides with your *arr stack.
- **Unpackerr:** Used to extract archived downloads automatically.
- **Plex Auto Languages:** Automatically switches audio/subtitle languages based on user preferences.
- **Whisparr:** Automated adult content management (part of the Servarr family).
- **Stash:** Adult media organizer with metadata scraping, tagging, and web-based streaming.
- **MeTube:** YouTube and web video downloader with browser extensions.
- **Homepage:** Modern dashboard to access all your services in one place.
- **Forgejo:** Self-hosted Git service for source code management (lightweight Gitea fork).
- **Gluetun:** VPN client container routing qBittorrent traffic through Surfshark WireGuard.
- **Authelia:** Single Sign-On and Two-Factor Authentication portal.
- **Vaultwarden:** Lightweight Bitwarden-compatible password manager.
- **Docker Socket Proxy:** Secure proxy for Docker socket access (replaces direct socket mounts).
- **WireGuard Easy:** Simple WireGuard VPN server with web UI.
- **Scrutiny:** Hard drive S.M.A.R.T. monitoring with web dashboard.
- **Gotify:** Self-hosted push notification server.
- **Maintainerr:** Automated Plex library maintenance and cleanup.
- **Speedtest Tracker:** Automated internet speed testing and history.
- **IT-Tools:** Collection of developer and networking utilities.
- **Mealie:** Recipe management and meal planning.
- **Actual Budget:** Privacy-focused personal finance and budgeting.

---

## Dependencies

1. Linux
2. Docker / Docker Compose
3. OPTIONAL: Portainer - Docker GUI

## How to Use

1. Clone this repository:
   ```bash
   git clone https://github.com/richardnixondev/homelab-ultimate-setup.git
   cd homelab-ultimate-setup
   ```

2. Create your `.env` file with required variables:
   ```bash
   cp .env.example .env
   nano .env
   ```

3. Rename the compose file:
   ```bash
   # For basic setup
   cp basic-compose.yaml docker-compose.yml

   # For advanced setup
   cp advanced-compose.yml docker-compose.yml
   ```

4. Start the stack:
   ```bash
   docker compose up -d
   ```

5. OPTIONAL: Setup a reverse proxy so you can use `radarr.my-domain.com` instead of IP addresses.

## Environment Variables

Required variables for the `.env` file:

| Variable | Example | Description |
|----------|---------|-------------|
| `PUID` | `1000` | User ID for container permissions |
| `GUID` | `1000` | Group ID for container permissions |
| `TZ` | `Europe/Dublin` | Timezone |
| `BASE_PATH` | `/mnt/truenas/config` | Config directory for all services |
| `DOCKER_PATH` | `/mnt/truenas/docker` | Persistent volumes directory |
| `MEDIA_SHARE` | `/mnt/truenas` | Root media storage path |
| `PLEX_CLAIM` | *(from plex.tv/claim)* | Plex server claim token |
| `PLEX_URL` | `http://IP:32400` | Local Plex URL |
| `PLEX_TOKEN` | *(your token)* | Plex authentication token |
| `SERVER_IP` | `10.10.11.201` | Server IP address |

## Folder Structure

To allow hardlinking to work (which you will definitely want!) you will have to use the same root folder in all of your container paths.

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

### Important Notes:

- In Radarr, set your category to "movies" - this will create the movies folder
- In Sonarr, set your category to "tv" - this will create the tv folder
- Always reference media folders as `/share/media/tv` instead of `/tv` for hardlinking to work

## Service Ports

| Service | Port | URL |
|---------|------|-----|
| Homepage | 3000 | http://IP:3000 |
| AdGuard Home | 3001 | http://IP:3001 |
| Traefik Dashboard | 8888 | http://IP:8888 |
| Plex | 32400 | http://IP:32400/web |
| Radarr | 7878 | http://IP:7878 |
| Sonarr | 8989 | http://IP:8989 |
| Prowlarr | 9696 | http://IP:9696 |
| Lidarr | 8686 | http://IP:8686 |
| Whisparr | 6969 | http://IP:6969 |
| Stash | 9998 | http://IP:9998 |
| qBittorrent | 8080 | http://IP:8080 |
| Seerr | 5055 | http://IP:5055 |
| Tautulli | 8181 | http://IP:8181 |
| Bazarr | 6767 | http://IP:6767 |
| Tdarr | 8265 | http://IP:8265 |
| Autobrr | 7474 | http://IP:7474 |
| Wizarr | 5690 | http://IP:5690 |
| Dozzle | 9999 | http://IP:9999 |
| Byparr | 8191 | http://IP:8191 |
| MeTube | 8081 | http://IP:8081 |
| Forgejo | 4000 | http://IP:4000 |
| Forgejo SSH | 2222 | ssh://git@IP:2222 |
| Authelia | 9091 | http://IP:9091 |
| Vaultwarden | 8222 | http://IP:8222 |
| Gluetun (Control) | 8000 | http://IP:8000 |
| WireGuard Easy | 51821 | http://IP:51821 |
| Scrutiny | 8082 | http://IP:8082 |
| Gotify | 8083 | http://IP:8083 |
| Maintainerr | 6246 | http://IP:6246 |
| Speedtest Tracker | 8084 | http://IP:8084 |
| IT-Tools | 8085 | http://IP:8085 |
| Mealie | 9925 | http://IP:9925 |
| Actual Budget | 5006 | http://IP:5006 |

---

## Known Issues & Workarounds

### Gluetun breaks Docker image pulls

Gluetun uses `NET_ADMIN` capability which modifies the host's iptables rules. This causes Docker to lose connectivity to container registries (`ghcr.io`, `lscr.io`, Docker Hub). The issue persists even after stopping Gluetun.

**Workaround — stop Gluetun before pulling images:**
```bash
# Stop VPN containers first
docker stop gluetun qbittorrent

# Pull images normally
docker compose -f advanced-compose.yml pull

# Restart everything
docker compose -f advanced-compose.yml up -d
```

If pulls still fail after stopping Gluetun, restart the Docker daemon:
```bash
sudo systemctl restart docker
docker compose -f advanced-compose.yml up -d
```

### Authelia pinned to v4.37

Authelia v4.38+ requires HTTPS for `authelia_url` in session cookie configuration. Since this homelab uses HTTP internally with `.homelab` domains (no TLS), Authelia is pinned to `authelia/authelia:4.37` which supports the legacy `domain` config without HTTPS. If you add TLS via Traefik in the future, you can upgrade to `latest`.

### Byparr zombie processes

Byparr spawns Camoufox/Firefox child processes that can accumulate as zombie processes (thousands over time). The `init: true` flag is set in compose to use tini as PID 1 and reap them automatically. Do not remove this flag.

---

## Sources and References

- [TRaSH Guides](https://trash-guides.info/) - Quality profiles and configuration guides
- [Servarr Wiki](https://wiki.servarr.com/) - Official *arr apps documentation
- [LinuxServer.io](https://www.linuxserver.io/) - Reliable Docker images
- [Kometa Wiki](https://kometa.wiki/) - Kometa documentation (formerly PMM)
- [Seerr Documentation](https://docs.seerr.dev/) - Seerr documentation
- [Whisparr Wiki](https://wiki.servarr.com/whisparr) - Whisparr documentation
- [Stash](https://stashapp.cc/) - Stash documentation
- [Homepage](https://gethomepage.dev/) - Homepage dashboard documentation
- [Hardlinks and Instant Moves](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) - Storage architecture guide
