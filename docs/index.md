# ADS-B Monitoring

Prometheus JSON Exporter mappings and Grafana dashboards for dump1090-fa aircraft, receiver health, and feeder units.

## Key features

- Live aircraft map and flight table through Grafana Infinity.
- Receiver message, signal, decode and CPU panels.
- Prometheus mappings for dump1090-fa stats and aircraft JSON.
- Feeder unit state from Node Exporter systemd metrics.

## Quick start

Open Grafana and import `dashboards/adsb-aircraft-viewer.json` through **Dashboards → New → Import**. Select the configured data source and match the dashboard variables to your labels. See [Getting started](getting-started.md) for prerequisites and setup.

## Where to next

<div class="wt-grid" markdown>

[:material-rocket-launch: **Getting started**<br>Set up the required integrations](getting-started.md){ .wt-card }

[:material-download: **Installation**<br>Install and connect the required services](installation.md){ .wt-card }

[:material-tune: **Configuration**<br>Review scrape examples and dashboard variables](configuration.md){ .wt-card }

[:material-sitemap: **Architecture**<br>Follow metrics from source to dashboard](architecture.md){ .wt-card }

[:material-view-dashboard: **Dashboard usage**<br>Import and use the dashboard](usage.md){ .wt-card }

</div>

## Support

{{ support() }}
