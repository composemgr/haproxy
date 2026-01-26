## 👋 Welcome to haproxy 🚀

Reliable, high-performance TCP/HTTP load balancer

## 📋 Description

Reliable, high-performance TCP/HTTP load balancer

## 🚀 Services

- **haproxy**: haproxy:latest

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/haproxy/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/haproxy" ~/.local/srv/docker/haproxy
cd ~/.local/srv/docker/haproxy
docker compose up -d
```

### Option 3: Using composemgr
```bash
composemgr install haproxy
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
```

See `docker-compose.yaml` for complete list of configurable options.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:8104

## 📂 Volumes

- `./rootfs/config/haproxy` - Data storage
- `./rootfs/data/haproxy` - Data storage

## 🔍 Logging

```shell
docker compose logs -f haproxy
```

## 🛠️ Management

```bash
# Start services
docker compose up -d

# Stop services
docker compose down

# Update to latest images
docker compose pull && docker compose up -d

# View logs
docker compose logs -f

# Restart services
docker compose restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
