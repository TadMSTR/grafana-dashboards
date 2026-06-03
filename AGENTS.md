# grafana-dashboards

Grafana dashboard JSON provisioning files for forge. No code.

## Structure

```
grafana-dashboards/
  unraid-array-monitoring/   Unraid array health panels
  unraid-system-v3/          Unraid system metrics v3
```

## What to know

- Each subdirectory is a Grafana provisioning dashboard folder.
- Files are standard Grafana JSON export format.
- Dashboards reference InfluxDB and other data sources by name — the data source name must match what is configured in the target Grafana instance.
- Do not embed credentials or internal IP addresses in dashboard JSON.
- Changes can be committed directly to `main` — this is a config-only repo.

## How to update

Export updated JSON from Grafana UI → "Dashboard settings" → "JSON model" → copy. Replace the file contents. Commit to main.
