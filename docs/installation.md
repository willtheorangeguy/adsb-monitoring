# adsb-monitoring — Installation

## Requirements

dump1090-fa, Prometheus Community JSON Exporter, Prometheus, Grafana; Infinity for the map; Node Exporter with the systemd collector for feeder state.

## Procedure

Install JSON Exporter with examples/json-exporter.yml. Point its receiver_stats and receiver_aircraft modules at the dump1090-fa stats.json and aircraft.json endpoints through the two /probe jobs in examples/prometheus-scrape.yml. Import the dashboard JSON files.

The files under [examples](../examples) are reference configuration. Replace example addresses, token paths and bind addresses for your deployment.

Next, review [configuration](./configuration.md) and [dashboard usage](./usage.md).
