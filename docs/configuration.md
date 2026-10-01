# Configuration

## Precedence

This repository combines dashboard defaults with settings for external services. It defines no shared command-line, environment variable and configuration-file override order; each external service resolves its own settings.

## Integration settings

The sample systemd unit expects /usr/local/bin/json_exporter and /etc/adsb-json-exporter.yml and listens on :9799. Replace sample receiver and exporter hosts. In Grafana set aircraft_json_url to a URL allowed by Infinity; select the Node Exporter instance and feeder service regex for the feeder panel.

## Dashboard variables

| Option | Type | Default | Description |
| --- | --- | --- | --- |
| `adsb-aircraft-viewer.json / prometheus_ds` | datasource | `prometheus` | Grafana data source selected by the dashboard. |
| `adsb-aircraft-viewer.json / infinity_ds` | datasource | `yesoreyeram-infinity-datasource` | Grafana data source selected by the dashboard. |
| `adsb-aircraft-viewer.json / job_adsb_receiver_aircraft` | textbox | `adsb-receiver-aircraft` | Dashboard variable whose value selects a scrape job, instance or endpoint. |
| `adsb-aircraft-viewer.json / job_adsb_receiver_stats` | textbox | `adsb-receiver-stats` | Dashboard variable whose value selects a scrape job, instance or endpoint. |
| `adsb-aircraft-viewer.json / aircraft_json_url` | textbox | `http://receiver.example:8080/data/aircraft.json` | Dashboard variable whose value selects a scrape job, instance or endpoint. |
| `adsb-feeder-stats.json / prometheus_ds` | datasource | `prometheus` | Grafana data source selected by the dashboard. |
| `adsb-feeder-stats.json / job_adsb_receiver_aircraft` | textbox | `adsb-receiver-aircraft` | Dashboard variable whose value selects a scrape job, instance or endpoint. |
| `adsb-feeder-stats.json / feeder_instance` | query | `label_values(node_systemd_unit_state, instance)` | Queries the data source for available values. |
| `adsb-feeder-stats.json / feeder_unit_regex` | textbox | `.*(feed\|feeder\|mlat\|piaware\|pfclient\|fr24).*\.service` | Filters Node Exporter systemd unit names for feeder services. |

## Prometheus jobs

The supplied [scrape example](https://github.com/willtheorangeguy/adsb-monitoring/blob/HEAD/examples/prometheus-scrape.yml) defines `adsb-receiver-stats`, `adsb-receiver-aircraft`, `node-exporter`. Copy its entries into your own scrape_configs and replace documentation hostnames. Job names can change if the dashboard variables change with them.

## Examples

The complete scrape job examples are in [`examples/prometheus-scrape.yml`](https://github.com/willtheorangeguy/adsb-monitoring/blob/HEAD/examples/prometheus-scrape.yml). Copy the relevant job into your Prometheus configuration and replace the example targets.
