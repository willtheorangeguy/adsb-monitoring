# adsb-monitoring — Quickstart

## Prerequisites

dump1090-fa, Prometheus Community JSON Exporter, Prometheus, Grafana; Infinity for the map; Node Exporter with the systemd collector for feeder state.

## Set up

Install JSON Exporter with examples/json-exporter.yml. Point its receiver_stats and receiver_aircraft modules at the dump1090-fa stats.json and aircraft.json endpoints through the two /probe jobs in examples/prometheus-scrape.yml. Import the dashboard JSON files.

The example Prometheus scrape job names are `adsb-receiver-stats`, `adsb-receiver-aircraft`, `node-exporter`.

## Confirm data

In Prometheus, check `up{job="adsb-receiver-stats"}`, `up{job="adsb-receiver-aircraft"}`, `up{job="node-exporter"}` and inspect a panel query in Grafana.
For missing data, see [troubleshooting](./troubleshooting.md).
