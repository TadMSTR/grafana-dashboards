# Unraid System Dashboard V3

**Comprehensive system monitoring for Unraid servers — CPU, memory, network, disk, temperatures, Docker, UPS, and log analysis.**

---

## Requirements

### Software Stack
- **Unraid 6.9+** (tested on 6.12+)
- **InfluxDB v2** — time-series metrics storage
- **Grafana** — dashboard platform (tested on 12.x)
- **Telegraf** — metrics collector running on Unraid host
- **Loki** — log aggregation
- **Promtail** — log shipper running on Unraid host

### Telegraf Plugins Required

| Plugin | Measurements | Notes |
|--------|-------------|-------|
| `inputs.cpu` | `cpu` | Per-core and total CPU usage |
| `inputs.mem` | `mem` | Memory used/cached/buffered/free |
| `inputs.system` | `system` | Load averages, uptime |
| `inputs.processes` | `processes` | Running and total process counts |
| `inputs.net` | `net` | Network bytes/packets per interface |
| `inputs.diskio` | `diskio` | Disk read/write bytes and ops |
| `inputs.disk` | `disk` | Disk space per mount point |
| `inputs.temp` | `temp` | CPU/system temperatures via lm-sensors |
| `inputs.smart` | `smart_device` | Drive temperatures and SMART data |
| `inputs.apcupsd` | `apcupsd` | UPS status, battery, load, runtime |
| `inputs.docker` | `docker`, `docker_container_cpu`, `docker_container_mem` | Container metrics (optional) |

### Loki Labels Required
Promtail must ship syslog with at least these labels:
- `host` — hostname (e.g. `unraid`)
- `job` — set to `syslog`

---

## Dashboard Panels

### UPS Row
- UPS Status (ONLINE / ON BATTERY)
- UPS Battery %
- UPS Load %
- Runtime Remaining (minutes)
- Est. Daily Power Cost (USD)
- Est. Monthly Power Cost (USD)

### System Stats Row
- System Uptime
- Total RAM
- RAM Used %
- Processes Running
- Total Processes
- Docker Container Count
- Network In / Network Out

### Timeseries
- CPU Usage (user / system / iowait / nice)
- System Load (1/5/15 min)
- Memory Usage (stacked: used / cached / buffered)
- CPU Usage Per Core (heatmap, all 32 threads)
- Network Traffic In/Out (bidirectional)
- Disk I/O (read up / write down, bytes/s)
- Disk I/O Ops/s (read up / write down)
- CPU / System Temperatures (lm-sensors)
- Disk Space Usage (bar gauge per mount point)
- Drive Temperatures HDD (per device, last + max in legend)
- Docker CPU Usage (per container)
- Docker Memory Usage (per container)

### Logs
- Log Error / Warning Rate — bar chart of error/warning/critical counts from syslog
- Syslog — live log panel filtered to errors, warnings, and criticals

---

## Dashboard JSON

Export the dashboard JSON from Grafana and save it to this directory as `dashboard.json`:

1. Open the dashboard in Grafana
2. Click the **Share** icon (top toolbar)
3. Select **Export**
4. Enable **Export for sharing externally** to replace datasource UIDs with template variables
5. Click **Save to file** and place the file here as `dashboard.json`

---

## Sample Configs

See `telegraf.conf` and `promtail.yml` in this directory for reference configurations.

### Power Cost

The daily and monthly cost panels use a hardcoded rate of **$0.2668/kWh**. Edit those panels in Grafana to update this for your rate.

### Network Interface

The Network In/Out stat panels are filtered to `eth0`. If your interface name differs, update the `interface` filter in those panels, or use the `$interface` dashboard variable.

### Docker

Docker panels require `inputs.docker` enabled in telegraf.conf with the Docker socket mounted. They are included but can be removed if not needed:

```toml
[[inputs.docker]]
  endpoint = "unix:///var/run/docker.sock"
```

### No Swap

Unraid does not use swap by default. Swap panels are intentionally excluded.

### PHP-FPM max_children

Unraid's built-in PHP-FPM defaults to 50 max_children which can be hit under load. Raise it and persist across reboots with a User Scripts startup script:

```bash
sed -i 's/pm.max_children = .*/pm.max_children = 100/' /etc/php-fpm.d/www.conf
/etc/rc.d/rc.php-fpm reload
```

---

## Notes

- Dashboard UID: `unraid-system-v2`
- Datasources required: InfluxDB (Flux), Loki
- Default time range: last 6 hours, auto-refresh 30s
- Tested on: Unraid 6.12, Grafana 12.3, InfluxDB 2.x, Loki 3.x
- Last updated: 2026-02-18
