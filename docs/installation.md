# Installation

## Requirements

dump1090-fa, Prometheus Community JSON Exporter, Prometheus, Grafana; Infinity for the map; Node Exporter with the systemd collector for feeder state.

## Procedure

Install JSON Exporter with examples/json-exporter.yml. Point its receiver_stats and receiver_aircraft modules at the dump1090-fa stats.json and aircraft.json endpoints through the two /probe jobs in examples/prometheus-scrape.yml. Import the dashboard JSON files.

The files under [examples](https://github.com/willtheorangeguy/adsb-monitoring/tree/HEAD/examples) are reference configuration. Replace example addresses, token paths and bind addresses for your deployment.

Next, review [configuration](configuration.md) and [dashboard usage](usage.md).

## Verify the installation

Check that the configured scrape target is healthy in Prometheus, then import the dashboard in Grafana and confirm its panels return data. Use the target and label names documented in [Getting started](getting-started.md).

## Upgrading

Update the dashboard JSON from this repository when you adopt a newer version. Update any exporter or monitored service using that project's upgrade instructions.

## Uninstalling

Remove the dashboard from Grafana and remove only the scrape or deployment entries you added for this project. Keep shared monitoring services that other dashboards use.
