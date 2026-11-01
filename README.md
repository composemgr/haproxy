## 👋 Welcome to haproxy 🚀

TCP and HTTP load balancer and reverse proxy

## 📋 Description

HAProxy is a fast and reliable open source load balancer and reverse proxy. This
stack ships the official HAProxy image with a configuration mounted from
`volumes/config/haproxy/haproxy.cfg`, and publishes the built-in statistics
interface on the assigned host port.

## 🚀 Services

- **app**: haproxy:latest

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/haproxy/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/haproxy" ~/.local/srv/docker/haproxy
cd ~/.local/srv/docker/haproxy
cp default.env .env
docker compose --env-file .env up -d
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

The proxy itself is configured in
`volumes/config/haproxy/haproxy.cfg`. Replace the placeholder credentials in the
`stats auth` line and define your own frontends and backends there.

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64193` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

## 🌐 Access

- **Statistics Interface**: http://172.17.0.1:64193

The HTTP/HTTPS listeners defined in `haproxy.cfg` are reachable from other
containers on the `haproxy` network, not from the host.

## 📂 Volumes

- `./volumes/config/haproxy/haproxy.cfg` - HAProxy configuration, read-only
- `./volumes/config/haproxy` - Lua scripts, read-only
- `./volumes/data/haproxy` - HAProxy runtime state

## 🔐 Security

- The statistics interface is protected by a `stats auth` line - always change
  the placeholder password
- HAProxy is published on the Docker host gateway only; do not expose it
  directly to the internet
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches

## 🔍 Logging

```shell
docker compose --env-file .env logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart

# Validate the configuration
docker compose --env-file .env exec app haproxy -c -f /usr/local/etc/haproxy/haproxy.cfg
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
