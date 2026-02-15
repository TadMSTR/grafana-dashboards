# Grafana Dashboards for Homelab

**Community-contributed Grafana dashboards for homelab monitoring**

---

## Overview

This repository contains production-ready Grafana dashboards specifically designed for homelab environments. Each dashboard includes:
- Complete setup instructions
- Required Telegraf configurations
- Dashboard JSON for import
- Screenshot examples

**Focus:** Self-hosted monitoring with InfluxDB + Grafana + Telegraf stack

---

## Available Dashboards

### Unraid Array Monitoring
**Metrics:** Storage, disk health, temperatures, UPS, power, growth predictions

![Unraid Dashboard Preview](./unraid-array-monitoring/screenshots/unraid-array-6hr.png)

**Features:**
- 15 comprehensive panels
- Array usage and growth tracking
- Per-disk usage and I/O monitoring
- Drive temperature trending
- UPS integration (battery, load, runtime)
- Power cost estimation
- Days until full prediction

**Ideal for:** Unraid servers with array storage, UPS monitoring

📁 [View Dashboard →](./unraid-array-monitoring/) | [Download JSON](./unraid-array-monitoring/grafana-unraid-dashboard.json)

---

## Tech Stack

**Required Components:**
- **InfluxDB v2** - Time-series database for metrics storage
- **Grafana** - Visualization and dashboard platform
- **Telegraf** - Metrics collection agent

**Supported Platforms:**
- Unraid (via Community Applications)
- TrueNAS Scale
- Docker on Linux
- Any system running Docker

---

## Quick Start

**1. Deploy InfluxDB + Grafana**
- Install via Docker Compose or your platform's app store
- Configure InfluxDB (organization, bucket, token)
- Connect Grafana to InfluxDB

**2. Install Telegraf on monitored host**
- Deploy Telegraf container
- Copy dashboard-specific config
- Verify metrics flowing to InfluxDB

**3. Import Dashboard**
- Download dashboard JSON
- Import to Grafana
- Customize as needed

**Detailed setup instructions are included with each dashboard.**

---

## Repository Structure

```
grafana-dashboards/
├── README.md (this file)
├── unraid-array-monitoring/
│   ├── README.md (setup instructions)
│   ├── dashboard.json (Grafana import)
│   ├── telegraf.conf (metrics collection config)
│   └── screenshots/ (dashboard examples)
└── [future dashboards]/
```

---

## Contributing

**Want to share your dashboard?**

Requirements:
- Production-tested dashboard
- Complete setup documentation
- Telegraf config (with sensitive data removed)
- At least one screenshot

**Submit via:**
- Pull request with dashboard folder
- Follow existing structure
- Include clear README

---

## Dashboard Guidelines

**What makes a good submission:**
- ✅ Comprehensive documentation
- ✅ Works out-of-box with provided configs
- ✅ Screenshots showing actual data
- ✅ Telegraf config included
- ✅ Sensitive data replaced with placeholders
- ✅ Tested on target platform

**Dashboard Standards:**
- Use descriptive panel titles
- Include units on gauges/stats
- Set appropriate thresholds
- Provide context in panel descriptions
- Use consistent color schemes

---

## Support

**Questions or Issues?**
- Open an issue in this repository
- Check dashboard-specific README first
- Include your platform details (Unraid/TrueNAS/etc.)

---

## Credits

**Created by:** TadMSTR  
**License:** MIT (dashboards can be freely used and modified)

---

## Changelog

**2026-02-15**
- Initial repository creation
- Added Unraid Array Monitoring dashboard

---

*Dashboards are provided as-is. Test in your environment before production use.*
