# adsb-monitoring — Configuration

The sample systemd unit expects /usr/local/bin/json_exporter and /etc/adsb-json-exporter.yml and listens on :9799. Replace sample receiver and exporter hosts. In Grafana set aircraft_json_url to a URL allowed by Infinity; select the Node Exporter instance and feeder service regex for the feeder panel.

## Dashboard variables

| Dashboard | Variable | Type | Default or query |
|---|---|---|---|
| `adsb-aircraft-viewer.json` | `prometheus_ds` | datasource | `prometheus` |
| `adsb-aircraft-viewer.json` | `infinity_ds` | datasource | `yesoreyeram-infinity-datasource` |
| `adsb-aircraft-viewer.json` | `job_adsb_receiver_aircraft` | textbox | `adsb-receiver-aircraft` |
| `adsb-aircraft-viewer.json` | `job_adsb_receiver_stats` | textbox | `adsb-receiver-stats` |
| `adsb-aircraft-viewer.json` | `aircraft_json_url` | textbox | `http://receiver.example:8080/data/aircraft.json` |
| `adsb-feeder-stats.json` | `prometheus_ds` | datasource | `prometheus` |
| `adsb-feeder-stats.json` | `job_adsb_receiver_aircraft` | textbox | `adsb-receiver-aircraft` |
| `adsb-feeder-stats.json` | `feeder_instance` | query | `label_values(node_systemd_unit_state, instance)` |
| `adsb-feeder-stats.json` | `feeder_unit_regex` | textbox | `.*(feed\|feeder\|mlat\|piaware\|pfclient\|fr24).*\\.service` |

## Prometheus jobs

The supplied [scrape example](../examples/prometheus-scrape.yml) defines `adsb-receiver-stats`, `adsb-receiver-aircraft`, `node-exporter`. Copy its entries into your own scrape_configs and replace documentation hostnames. Job names can change if the dashboard variables change with them.
