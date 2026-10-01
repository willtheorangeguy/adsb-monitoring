<h1 align="center">adsb-monitoring</h1>
<h4 align="center">Prometheus JSON Exporter mappings and Grafana dashboards for dump1090-fa aircraft, receiver health, and feeder units.</h4>

<div align="center">
  <img alt="GitHub Issues" src="https://img.shields.io/github/issues/willtheorangeguy/adsb-monitoring">
  <img alt="GitHub Pull Requests" src="https://img.shields.io/github/issues-pr/willtheorangeguy/adsb-monitoring">
  <img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-blue">
  <img alt="gitleaks workflow" src="https://github.com/willtheorangeguy/adsb-monitoring/actions/workflows/gitleaks.yml/badge.svg">
  <img alt="testing workflow" src="https://github.com/willtheorangeguy/adsb-monitoring/actions/workflows/testing.yml/badge.svg">
</div>

<p align="center">
  <a href="#key-features">Key Features</a> •
  <a href="#installation">Installation</a> •
  <a href="#usage">Usage</a> •
  <a href="#documentation">Documentation</a> •
  <a href="#support">Support</a> •
  <a href="#contributing">Contributing</a> •
  <a href="#license">License</a>
</p>

<!-- Screenshot: after adding adsb-monitoring/overview.png to .github/icons/, replace this comment with ![Dashboard overview](https://raw.githubusercontent.com/willtheorangeguy/.github/main/icons/adsb-monitoring/overview.png). -->

Prometheus JSON Exporter mappings and Grafana dashboards for dump1090-fa aircraft, receiver health, and feeder units.

## Key Features

- Live aircraft map and flight table through Grafana Infinity.
- Receiver message, signal, decode and CPU panels.
- Prometheus mappings for dump1090-fa stats and aircraft JSON.
- Feeder unit state from Node Exporter systemd metrics.

## Installation

dump1090-fa, Prometheus Community JSON Exporter, Prometheus, Grafana; Infinity for the map; Node Exporter with the systemd collector for feeder state. Install JSON Exporter with examples/json-exporter.yml. Point its receiver_stats and receiver_aircraft modules at the dump1090-fa stats.json and aircraft.json endpoints through the two /probe jobs in examples/prometheus-scrape.yml. Import the dashboard JSON files. See [installation](docs/installation.md) for more detail.

## Usage

Import [adsb-aircraft-viewer.json](dashboards/adsb-aircraft-viewer.json), [adsb-feeder-stats.json](dashboards/adsb-feeder-stats.json) in Grafana using **Dashboards → New → Import**. Choose the data source and match the dashboard variables to your monitoring labels. See [dashboard usage](docs/usage.md).

## Documentation

Full documentation lives in [docs/](docs/index.md): [Quickstart](docs/getting-started.md) · [Configuration](docs/configuration.md) · [Architecture](docs/architecture.md) · [Dashboard usage](docs/usage.md) · [Troubleshooting](docs/troubleshooting.md).

## Support

Open a [GitHub Discussion](https://github.com/willtheorangeguy/adsb-monitoring/discussions/new) or file an [issue](https://github.com/willtheorangeguy/adsb-monitoring/issues/new/choose).

## Contributing

Contributions welcome. See the org-wide [Contributing Guide](https://github.com/willtheorangeguy/.github/blob/main/CONTRIBUTING.md) and [Code of Conduct](https://github.com/willtheorangeguy/.github/blob/main/CODE_OF_CONDUCT.md).

## License

MIT — see [LICENSE.md](LICENSE.md).
