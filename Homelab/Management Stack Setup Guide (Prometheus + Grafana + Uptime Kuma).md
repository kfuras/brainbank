This guide walks you through setting up a Docker-based monitoring stack with Prometheus, Grafana, and Uptime Kuma in a homelab environment. The setup is structured using a dedicated `management-stack` Docker Compose file.

## Directory Structure

```Shell
~/docker/management-stack/
├── appdata/
│   ├── grafana/
│   ├── prometheus/
│   │   ├── data/
│   │   └── prometheus.yml
│   └── uptime-kuma/
└── docker-compose.yml
```

## .env File

Place this `.env` file in the same folder as your `docker-compose.yml`:

```Plain
PROMETHEUS_PORT=9090
GRAFANA_PORT=3000
UPTIME_KUMA_PORT=3001
GRAFANA_USER=admin
GRAFANA_PASSWORD=changeme
```

## prometheus.yml

Place this file under `./appdata/prometheus/prometheus.yml`:

```YAML
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: "prometheus"
    static_configs:
      - targets: ["localhost:9090"]
        labels:
          stack: management

  - job_name: "cadvisor"
    static_configs:
      - targets: ["cadvisor:8080"]
        labels:
          stack: management

  - job_name: "media-stack"
    static_configs:
      - targets:
          - "radarr:7878"
          - "sonarr:8989"
          - "jackett:9117"
          - "qbittorrent:8080"
          - "plex:32400"
          - "unpackerr:5656"
        labels:
          stack: media

  - job_name: "unifi-stack"
    static_configs:
      - targets:
          - "unifi-controller:8443"
        labels:
          stack: unifi

  - job_name: "management-stack"
    static_configs:
      - targets:
          - "uptime-kuma:3001"
        labels:
          stack: management
```

## docker-compose.yml

```YAML
services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    restart: unless-stopped
    ports:
      - "${PROMETHEUS_PORT}:9090"
    volumes:
      - ./appdata/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml:ro
      - ./appdata/prometheus/data:/prometheus
    networks:
      - management-net
      - unifi-net
      - media-net

  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    restart: unless-stopped
    ports:
      - "${GRAFANA_PORT}:3000"
    environment:
      - GF_SECURITY_ADMIN_USER=${GRAFANA_USER}
      - GF_SECURITY_ADMIN_PASSWORD=${GRAFANA_PASSWORD}
    volumes:
      - ./appdata/grafana:/var/lib/grafana
    networks:
      - management-net
      - unifi-net
      - media-net

  uptime-kuma:
    image: louislam/uptime-kuma:latest
    container_name: uptime-kuma
    restart: unless-stopped
    ports:
      - "${UPTIME_KUMA_PORT}:3001"
    volumes:
      - ./appdata/uptime-kuma:/app/data
    networks:
      - management-net
      - unifi-net
      - media-net

networks:
  management-net:
    external: true
  unifi-net:
    external: true
  media-net:
    external: true
```

## First-time Setup Steps

1. **Create Docker Networks** (if not already created):

```Shell
docker network create management-net
docker network create media-net
docker network create unifi-net
```

1. **Start the Stack**:

```Shell
docker compose up -d
```

---

## Troubleshooting

### Grafana - Permission Denied

If Grafana logs show errors like:

```Plain
GF_PATHS_DATA='/var/lib/grafana' is not writable.
mkdir: can't create directory '/var/lib/grafana/plugins': Permission denied
```

**Fix it by running:**

```Shell
sudo chown -R 472:472 ./appdata/grafana
```

### Prometheus - mmap query log failure

If Prometheus fails to start with:

```Plain
Error opening query log file /prometheus/queries.active: permission denied
panic: Unable to create mmap-ed active query log
```

**Fix it by setting correct ownership:**

```Shell
sudo chown -R 65534:65534 ./appdata/prometheus/data
```

Then restart:

```Shell
docker compose down && docker compose up -d
```

---

## Next Steps

- Open Grafana on `http://<host>:3000`
- Add Prometheus as a data source (`http://prometheus:9090`)
- Start creating dashboards or import community ones
- Access Prometheus via `http://<host>:9090`
- Access Uptime Kuma via `http://<host>:3001`