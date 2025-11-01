
### Simple Docker-based monitoring setup powered by Prometheus and Grafana.

### Core tools:
- Prometheus (Gather (Collects) All Metrics)
- Grafana (Visualising for humans as well alerting)

### Additional tools
##### These below send metrics (data) to (as an example) Prometheus
##### Exporters:
**node-exporter** — system metrics

**cAdvisor** — container metrics

**blackbox-exporter** — endpoint probing

**zabbix-agent** — extra host metrics

_All Deployed with Docker Compose_

All details see in core files: ```docker-compose.yml```

_Hoped further updates coming soon ..._
