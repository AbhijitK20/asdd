# Practical 7 — Monitoring using Grafana

**Aim:** To monitor system and application metrics using Grafana dashboards.

**Prerequisite:** A Grafana installation (or Docker). A data source such as
Prometheus is recommended but optional for a first dashboard.

---

## Install Grafana

Choose one:

**Docker (fastest):**

```bash
cd docker
docker compose up -d grafana
```

Or directly:

```bash
docker run -d --name=grafana -p 3000:3000 grafana/grafana
```

**Linux (Debian/Ubuntu):**

```bash
sudo apt-get install -y apt-transport-https
sudo apt-get install -y grafana
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
```

**Windows:**

1. Download the `.msi` from https://grafana.com/grafana/download.
2. Run the installer → Next → Install.
3. Start the service: `net start Grafana`.

## Log in

1. Open http://localhost:3000.
2. Default credentials: **admin / admin**.
3. Grafana asks you to set a new password — do it.

> On Linux/Docker the port is 3000; if it is busy, map another one
> (`-p 3001:3000`) and open http://localhost:3001.

## Add a data source

1. Left menu → **Connections** → **Data sources** → **Add data source**.
2. Choose **Prometheus**.
3. Connection URL: `http://localhost:9090` (or `http://prometheus:9090` when
   both run in Docker on the same network).
4. **Save & test** → "Data source is working".

> No Prometheus? Skip this step and use the **TestData** data source
> (built-in) to create a demo dashboard.

## Create a dashboard

1. **Dashboards** → **New** → **New dashboard** → **Add visualization**.
2. Pick the data source.
3. Enter a query, e.g. PromQL:
   `rate(node_cpu_seconds_total{mode="system"}[1m])`
4. Choose a visualization type (Time series, Gauge, Stat, Table).
5. Set the unit (percent, seconds, bytes) and thresholds (green/yellow/red).
6. **Apply** → **Save dashboard** → name it `ASDD Monitoring`.
7. Add a second panel (e.g. memory or request rate).

## Add an alert rule

1. **Alerting** → **Alert rules** → **New alert rule**.
2. Select the data source and query (e.g. CPU > 80%).
3. Set the condition and evaluation interval.
4. Choose a contact point (email, Slack, webhook).
5. **Save rule and exit**.

## What to verify / screenshot

- [ ] Grafana login page / dashboard home
- [ ] Data source showing "working"
- [ ] Dashboard with at least two panels
- [ ] Panel edit screen showing the query
- [ ] An alert rule

## Troubleshooting

| Problem | Fix |
|---|---|
| `Connection refused` on 3000 | Grafana not started: `sudo systemctl status grafana-server` or `docker ps` |
| Forgot admin password | `grafana-cli admin reset-admin-password <new>` (or `docker exec -it grafana grafana-cli admin reset-admin-password <new>`) |
| Port 3000 busy | Map `-p 3001:3000` and open the new port |
| Data source fails | Prometheus must be running and reachable from the Grafana container/network |
| No data in panels | Check the time range (top-right) and the query |

## Viva

- **Grafana vs Prometheus?** Prometheus collects/stores metrics; Grafana visualises and alerts on them.
- **What is a data source?** The backend Grafana queries (Prometheus, InfluxDB, MySQL, …).
- **What is a panel?** A single visualisation inside a dashboard.
- **What language do Prometheus queries use?** PromQL.
- **What is an alert rule?** A condition on a query that fires a notification when true.

**Result:** System/application metrics were visualised on Grafana dashboards and
an alert rule was configured successfully.
