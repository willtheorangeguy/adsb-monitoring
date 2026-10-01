# dump1090-fa JSON Exporter mapping and ADS-B aircraft and feeder dashboards

Portable monitoring bundle with example configuration. Replace example addresses and token paths for your installation; no live credentials are included.

## Requirements

dump1090-fa, Prometheus Community JSON Exporter, Node Exporter systemd collector for feeder state, and Grafana Infinity for the live aircraft viewer.

## Dashboards

- `dashboards/adsb-aircraft-viewer.json`
- `dashboards/adsb-feeder-stats.json`

Import the JSON in Grafana using **Dashboards > New > Import**. Select your data source from the dashboard variable(s) at the top. Update the Prometheus job variables to match your `scrape_configs` job names; use the Instance selector when present. The dashboard's JSON is also suitable for file provisioning after you have selected or provisioned data source UIDs.

Expected default job labels:

- `adsb-aircraft-viewer.json`: adsb-receiver-aircraft, adsb-receiver-stats
- `adsb-feeder-stats.json`: adsb-receiver-aircraft

Set `aircraft_json_url` to the receiver's reachable `/data/aircraft.json` URL and allow that host in your Infinity data source. Set the Node Exporter instance and feeder service regex used for feeder state. The feeder dashboard adapts the intent of Grafana.com dashboard 18398; retain attribution when publishing.

## Monitoring code

See the code and example configuration in this folder, if present. Keep API keys and metrics bearer tokens in local secret files or another secret manager; never commit them. Scrape examples use documentation addresses and must be edited for your network.

## Before publishing

Test against the application and Grafana versions you intend to support. Add a license you choose and check attribution for upstream components. No release or Grafana catalog upload has been performed.

## Receiver setup

Install Prometheus Community `json_exporter` and supply `examples/json-exporter.yml`. Configure two Prometheus scrapes through its `/probe` endpoint: `receiver_stats` against your dump1090-fa `stats.json` as job `adsb-receiver-stats`, and `receiver_aircraft` against `aircraft.json` as job `adsb-receiver-aircraft`. Change the dashboard job variables if your jobs differ. `examples/json-exporter.service` is a starting systemd unit and binds all interfaces; restrict network access before using it outside a trusted network. For the live aircraft viewer, configure Grafana Infinity with the receiver host on its allowed-host list, then set the dashboard's `aircraft_json_url` variable. Node Exporter's systemd collector supplies feeder-unit state to the second dashboard.

A sample `scrape_configs` fragment is in `examples/prometheus-scrape.yml`; replace the example hosts and token paths.
