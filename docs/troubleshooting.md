# adsb-monitoring — Troubleshooting

| Symptom | Check |
|---|---|
| Map blank | allow the receiver host in Infinity and check aircraft_json_url. |
| Feeder panel blank | enable the Node Exporter systemd collector and select the correct instance and unit regex. |
| Snapshot age rising | inspect the aircraft probe and dump1090-fa JSON endpoint. |

## First checks

Check the selected Grafana data source and dashboard variables in [configuration](./configuration.md). For Prometheus, inspect the target state and the exact job and instance labels before changing panel queries.
