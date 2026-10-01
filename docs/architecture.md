# adsb-monitoring — Architecture

dump1090-fa JSON -> JSON Exporter /probe -> Prometheus -> Grafana. Infinity fetches aircraft.json for the live map and table. Node Exporter supplies node_systemd_unit_state.

## Components

- [dashboards/](../dashboards): Grafana dashboard definitions
- [examples/](../examples): deployment and scrape examples

## Data interpretation

The map may work while the Prometheus probes fail, or vice versa. Feeder active state does not prove remote sites accepted data. The feeder dashboard adapts Grafana.com dashboard 18398; retain attribution.
