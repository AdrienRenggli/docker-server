# 🐳 docker-server

Docker configuration for my homelab server. This repository contains various self-hosted services ranging from home security to network management and personal finance.

---

## 🖥️ Hardware & Host Specs

* **Hardware:** Beelink SER8 Mini PC
* **Memory:** 32 GB RAM
* **Storage Strategy:** Core application configurations and databases persist in `/data`. Dedicated external media and backup libraries are mounted under `/mnt/media` and `/mnt/immich-storage`. To optimize power consumption and reduce drive wear, external drives can be configured to spin down (sleep) after a defined period of inactivity (e.g., using tools like `hdparm` or `hd-idle`).

---

## 🛠️ Services Overview

| Category | Services | Description |
| :--- | :--- | :--- |
| **Entertainment** | `Jellyfin`, `Seerr`, `Minecraft` | High-performance media streaming and media browser, local Minecraft server. |
| **Home Ops** | `Frigate`, `ESPHome`, `Spoolman` | AI-powered NVR with object and people recognition, microcontrollers turned into smart devices, local database for 3D filament. |
| **Network** | `Pi-hole`, `WireGuard`, `DuckDNS`, `NPM` | Network-wide ad blocking, secure remote VPN access, Dynamic DNS, Nginx Proxy Manager. |
| **Photos** | `Immich` | Self-hosted backup solution for photos and videos. |
| **Office** | `Firefly III`, `Nextcloud`, `ONLYOFFICE` | Personal finance, local cloud, and office suite. |
| **AI** | `Ollama`, `Open WebUI` | Local AI models and chat interface. Auto-pulls `qwen2.5-coder:7b`, `llama3.1:8b`, `qwen2.5:14b`, and `nomic-embed-text` embeddings. |
| **Torrent** | `qBittorrent`, `gluetun` | Torrent downloader routed through a VPN killswitch. |
| **Utilities** | `Homepage`, `UpSnap`, `WUD` | Service dashboard, Wake-on-LAN, and update monitoring. |

---

## 🚀 Getting Started

### 1. Prerequisites

* **Docker & Compose**: Ensure Docker and the Compose plugin are installed on your server.
* **Storage**: This configuration expects data to be stored primarily in `/data`. Media and photos are stored on external disks mounted at `/mnt/media` and `/mnt/immich-storage`.


* **Disk Spindown (Optional)**: If you are using mechanical hard drives for `/mnt/media` or backups, you can configure sleep timeouts via `hdparm -S <timeout> /dev/sdX` or `hd-idle` so the disks power down when idle.
* **Hardware Access**: Services like Frigate, Ollama, or Jellyfin require device permissions (e.g., `/dev/dri` for GPU hardware acceleration).


* **Portainer (Optional)**: To manage Docker through a web interface.

### 2. Configuration

Sensitive information is managed via `stack.env` files, which are excluded from version control.

1. Navigate to the desired service directory (e.g., `cd pi-hole/`).


2. Create a local environment file from the provided template:
    ```bash
    cp stack.example stack.env
    ```

3. Edit `stack.env` with your specific credentials (IP addresses, API tokens, passwords).



### 3. Deployment

Deploy individual stacks by running the following command from within the service folder:

```bash
docker compose up -d
```

---

## 🔐 Key Features

* **Automated AI Setup:** The Ollama stack automatically downloads and prepares the `qwen2.5-coder:7b`, `llama3.1:8b`, `qwen2.5:14b`, and `nomic-embed-text` models on initial launch.


* **Updates:** `WUD` (What's Up Docker) monitors containers and sends notifications (e.g., via Discord).


* **Network Privacy:** `Pi-hole` handles DNS-level ad-blocking, while `WireGuard` provides encrypted remote access to your home network.


* **Hardware Acceleration:** `Jellyfin` and `Frigate` are configured to use `/dev/dri` for video transcoding and detection.


* **Security:** All `stack.env` files are ignored by git to prevent leaking credentials.

---

## 📂 Project Structure

```plaintext
.
├── cloud-office/     # Nextcloud and ONLYOFFICE
├── duckdns/          # Dynamic DNS (DuckDNS)
├── esp_home/         # Microcontroller programmer for smart devices
├── firefly-iii/      # Financial manager
├── frigate/          # AI NVR
├── homepage/         # Application dashboard
├── immich/           # Photo management
├── jellyfin/         # Media server and browser
├── minecraft/        # Local Minecraft server
├── npm/              # Nginx Proxy Manager
├── ollama/           # Local AI models and web interface
├── pi-hole/          # DNS ad-blocker
├── spoolman/         # 3D filament database  
├── upsnap/           # Wake-on-LAN
├── wireguard/        # VPN server
└── wud/              # Container update monitoring

```

---

## 💬 Configuration Help

I don't share active configuration files for privacy reasons. However, feel free to open an issue or reach out if you need help organizing or configuring these stacks!