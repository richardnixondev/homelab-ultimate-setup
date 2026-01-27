# <img src="/ultimate_plex_stack_transparent_bg.png" width="300px" alt="The Ultimate Plex Stack"></img>

> **Fork Notice:** Este repositório é um fork do [ultimate-plex-stack](https://github.com/DonMcD/ultimate-plex-stack) original. O objetivo deste fork é modernizar o stack, substituindo ferramentas deprecadas por alternativas atuais e mantendo as melhores práticas de 2025/2026.

Welcome to my stack repository! This repository showcases my docker compose setup for managing various media-related services using Docker containers. The compose file is meant to be modified to each user's liking as I know, not everyone has the same requirements.

Currently you can choose from the **Basic** or the **Advanced** compose.

---

## Análise de Ferramentas (2025/2026)

### Legenda de Status

| Status | Significado |
|--------|-------------|
| :white_check_mark: | Ativo e recomendado |
| :warning: | Funcional, mas com ressalvas |
| :x: | Deprecado - substituir |
| :arrows_counterclockwise: | Migração recomendada |

### Análise Detalhada

| Ferramenta | Status | Análise | Recomendação |
|------------|--------|---------|--------------|
| **Plex** | :white_check_mark: | Continua sendo o media server mais polido e user-friendly. Suporte extensivo a dispositivos. Plex Pass opcional para recursos avançados. | Manter. Alternativas: [Jellyfin](https://jellyfin.org/) (open-source, gratuito) ou [Emby](https://emby.media/). |
| **Radarr** | :white_check_mark: | Ativamente mantido. Parte do ecossistema Servarr. | Manter. |
| **Sonarr** | :white_check_mark: | Ativamente mantido. Requer v4+. | Manter. |
| **Prowlarr** | :white_check_mark: | Ativamente mantido. Suporta 500+ trackers torrent e 24+ indexers Usenet. | Manter. |
| **Readarr** | :white_check_mark: | Branch `develop` ainda é necessário para algumas funcionalidades. | Manter. |
| **Lidarr** | :white_check_mark: | Ativamente mantido para automação de música. | Manter. |
| **qBittorrent** | :white_check_mark: | Ranked #1 entre clientes torrent. Suporta até 10.000 torrents. | Manter. Alternativas: [Transmission](https://transmissionbt.com/) (mais leve), [Deluge](https://deluge-torrent.org/) (mais customizável via plugins). |
| **Overseerr** | :arrows_counterclockwise: | Sendo **deprecado** e fundido com Jellyseerr em um novo projeto chamado **Seerr**. | **Migrar para [Seerr](https://github.com/seerr-team/seerr)** - suporta Plex, Jellyfin e Emby. |
| **Plex Meta Manager** | :x: | **DEPRECADO** em Abril 2024. Projeto renomeado para Kometa. LinuxServer.io não oferece mais suporte à imagem antiga. | **Substituir por [Kometa](https://github.com/Kometa-Team/Kometa)** (`kometateam/kometa`). |
| **Tdarr** | :warning: | Funcional e poderoso para transcoding distribuído. Closed-source. | Manter. Alternativa open-source: [Unmanic](https://github.com/Unmanic/unmanic). |
| **Tautulli** | :white_check_mark: | Continua sendo a melhor ferramenta de monitoramento para Plex. Alguns antivírus podem gerar falsos positivos. | Manter. |
| **Bazarr** | :white_check_mark: | Ativamente mantido. Suporte a Python 3.13+. Integração com OpenSubtitles melhorada. | Manter. |
| **Autobrr** | :white_check_mark: | Ativamente mantido (Go 1.25+). Melhor opção para IRC automation. | Manter. |
| **Flaresolverr** | :arrows_counterclockwise: | Cloudflare atualiza constantemente suas proteções. FlareSolverr tem dificuldades em acompanhar. | **Considerar migrar para [Byparr](https://github.com/ThePhaseless/Byparr)** - drop-in replacement mais moderno usando Camoufox. |
| **Membarr** | :warning: | Projeto original pode estar abandonado. Forks da comunidade (Yoruio/Membarr) continuam disponíveis. | Avaliar se Wizarr não atende melhor a necessidade. |
| **Wizarr** | :white_check_mark: | Ativamente mantido (v2025.10.5+). Suporta Plex, Jellyfin, Emby, Audiobookshelf, Romm, Komga e Kavita. | Manter. |
| **Dozzle** | :white_check_mark: | Leve e eficiente para logs em tempo real. Suporta Docker, Swarm, K8s, Podman. | Manter. Para logs históricos/search, considerar [Loki + Grafana](https://grafana.com/oss/loki/). |
| **Plex Auto Languages** | :warning: | Projeto original (RemiRigal) pode ter sido abandonado. Forks da comunidade (JourneyDocker, thesammykins) continuam. Problemas reportados em TrueNAS Scale. | Usar fork ativo: `journeyover/plex-auto-languages` ou rewrite em TypeScript de thesammykins. |
| **Cross-Seed** | :white_check_mark: | Ativamente mantido (v6). Suporta qBittorrent, rTorrent, Deluge, Transmission. | Manter. |
| **Unpackerr** | :white_check_mark: | Ativamente mantido. Suporta RAR, ZIP, 7ZIP, TAR e mais. Auto-detecção de *arr apps. | Manter. |
| **Recyclarr** | :white_check_mark: | Ativamente mantido. TRaSH Guides atualizados em Janeiro 2026. Suporta Radarr e Sonarr v4+. | Manter. |

---

## Mudanças Prioritárias para Modernização

### :x: Substituições Obrigatórias

1. **Plex Meta Manager → Kometa**
   ```yaml
   # Antes (deprecado)
   plex-meta-manager:
     image: meisnate12/plex-meta-manager

   # Depois
   kometa:
     image: kometateam/kometa
   ```

2. **Overseerr → Seerr**
   ```yaml
   # Antes (será deprecado)
   overseerr:
     image: lscr.io/linuxserver/overseerr:latest

   # Depois
   seerr:
     image: ghcr.io/seerr-team/seerr:latest
   ```

### :arrows_counterclockwise: Migrações Recomendadas

3. **Flaresolverr → Byparr** (se enfrentando problemas com Cloudflare)
   ```yaml
   # Alternativa mais moderna
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
- **Overseerr:** Request management and monitoring for Plex.
- **Qbittorrent:** BitTorrent client with VPN support.

**Advanced Compose** Includes:

- **Plex:** Media server for streaming movies and TV shows.
- **Radarr:** Movie management and automation.
- **Sonarr:** TV show management and automation.
- **Prowlarr:** Indexer manager for Radarr and Sonarr.
- **Overseerr:** Request management and monitoring for Plex.
- **Qbittorrent:** BitTorrent client with VPN support.
- **Tdarr:** Pre-transcodes your media to decrease file sizes
- **Membarr:** Invite users to your Plex via discord
- **Tautulli:** Analytics and monitoring for Plex.
- **Bazarr:** Subtitle management for movies and TV shows.
- **Autobrr:** Used to grab torrents immediately as they are released.
- **Readarr:** Used to grab books and audiobooks.
- **Lidarr:** Used to grab music.
- **Flaresolverr:** Used as a proxy server to bypass Cloudflare and DDoS-GUARD protection.
- **Dozzle:** Used to view the logs of any container.
- **Wizarr:** Used to create links that can be sent to users so they can be invited to your media server.
- **Kometa:** Used to create collections, overlays, playlists and much more! *(Formerly Plex Meta Manager)*
- **Plex Auto Languages:** Used to auto update the language of your Plex TV episodes
- **Recyclarr:** Used to sync the config of trash guides with your arr stack


## Dependencies

1. Linux
2. Docker / Docker Compose
3. OPTIONAL: Portainer - Docker GUI

## How to Use

1. Clone this repository / Copy the docker-compose.yml file:

   ```
   git clone https://github.com/richardnixondev/homelab-ultimate-setup.git
   ```
2. Rename the advanced-compose or basic-compose to docker-compose.yml
3. Fill in the required environment variables
5. Then enter the command ``` docker compose up -d ```
6. OPTIONAL: Setup a reverse proxy so you can use radarr.my-domain.com instead of 192.168..... to access each of your apps

## Example of Environment variables in Portainer
Keep in mind some variable names have changed since this screenshot was taken
<img width="657" alt="image" src="https://github.com/DonMcD/ultimate-plex-stack/assets/90471623/9a614eb0-8ff7-4eb9-b154-61c08cd595e9">


File location examples:
- {MEDIA_SHARE} = /share
- {BASE_PATH} = /home/username/docker

To allow hardlinking to work (which you will definitely want!) you will have to use the same root folder in all of your container path. In this example we use "/share", so in the container it will look like "/share/downloads/tv"

An example of my folder structure:
![image](https://github.com/DonMcD/ultimate-plex-stack/assets/90471623/2003ac26-a929-4ff6-ad67-e35fc51fb51a)

- Feel free to expand your folders to also include "books" or "music" as you need for your setup



1. In Radarr you will want to set your category to "movies", this will create the movies folder
2. In Sonarr you will want to set your category to "tv", this will create the tv folder


Anytime you reference your media folder in a container you want the path to look like /share/media/tv instead of /tv like a lot of the default guides say, if you do end up mapping the path as /tv hardlinking will not work

## Possible Additions

1. Organizr - Creates a lovely dashboard to help navigate to all of your apps
2. Portainer - Docker GUI
3. UptimeKuma - Gives you the ability to monitor your services
4. [Homarr](https://homarr.dev/) - Modern dashboard alternative to Organizr
5. [Homepage](https://gethomepage.dev/) - Another modern dashboard option

---

## Fontes e Referências

- [TRaSH Guides](https://trash-guides.info/) - Guias de qualidade e configuração
- [Servarr Wiki](https://wiki.servarr.com/) - Documentação oficial dos *arr apps
- [LinuxServer.io](https://www.linuxserver.io/) - Imagens Docker confiáveis
- [Kometa Wiki](https://kometa.wiki/) - Documentação do Kometa (ex-PMM)
- [Seerr Documentation](https://docs.seerr.dev/) - Documentação do Seerr
