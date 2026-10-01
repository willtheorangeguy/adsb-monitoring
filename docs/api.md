# adsb-monitoring — Metric Sources and Endpoints

dump1090-fa JSON -> JSON Exporter /probe -> Prometheus -> Grafana. Infinity fetches aircraft.json for the live map and table. Node Exporter supplies node_systemd_unit_state.

## Interfaces

- JSON Exporter `/probe` uses `receiver_stats` and `receiver_aircraft` from [json-exporter.yml](../examples/json-exporter.yml).
- dump1090-fa serves `/data/stats.json` and `/data/aircraft.json`.

## Prometheus scrape reference

See [examples/prometheus-scrape.yml](../examples/prometheus-scrape.yml) for the target, job name and authorization settings.

## JSON mapping

The `receiver_stats` module maps completed one-minute decoder windows into message, track, signal, noise, gain, CPR outcome and CPU metrics. The `receiver_aircraft` module maps the current snapshot into `adsb_aircraft_in_view`, `adsb_aircraft_position_available`, `adsb_aircraft_callsign_available` and `adsb_aircraft_emergency_7700_active`, each labeled by aircraft hex identifier. It also exports `adsb_aircraft_snapshot_seconds`. The complete paths and HELP text are in [json-exporter.yml](../examples/json-exporter.yml).
