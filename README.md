
# monitoring-core-stack

Simple Docker Compose based monitoring stack.

## What is here

- `prometheus/` - Prometheus, Grafana and local node-exporter.
- `cadvisor_blackbox/` - cAdvisor and blackbox-exporter for remote probing hosts.

## Git remotes

- `origin` - GitHub: `git@github.com:garbolovo/monitoring-core-stack.git`
- `server` - bare repo on the monitoring server: `ssh://root@194.226.49.20/var/repo/monitoring-core-stack.git`

At the last local check both remotes had the same `master` commit.

## Prometheus stack

The main stack is in `prometheus/docker-compose.yml`.

```bash
cd prometheus
docker compose up -d
docker compose ps
docker compose logs -f prometheus
```

Services:

- Grafana: `http://<host>:3000`
- Prometheus: `http://<host>:9090`
- node-exporter: `http://<host>:9100/metrics`

Prometheus reads `prometheus/prometheus.yml` from the repository as a read-only bind mount.

## Exporters stack

The remote exporter stack is in `cadvisor_blackbox/docker-compose.yml`.

```bash
cd cadvisor_blackbox
docker compose up -d
docker compose ps
```

Services:

- cAdvisor publishes host/container metrics on port `8081`.
- blackbox-exporter publishes probe metrics on port `9115`.

The blackbox modules are defined in `cadvisor_blackbox/blackbox.yml`. Prometheus currently expects the same modules on the configured blackbox hosts.

## Useful checks

```bash
docker compose -f prometheus/docker-compose.yml config
docker compose -f cadvisor_blackbox/docker-compose.yml config
```

If `promtool` is installed, also run:

```bash
promtool check config prometheus/prometheus.yml
```
