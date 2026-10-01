# Dashboard usage

Import the JSON files using **Grafana → Dashboards → New → Import**. Set the data source and variables listed in [configuration](configuration.md).

## ADS-B Aircraft Viewer

Source: [`dashboards/adsb-aircraft-viewer.json`](https://github.com/willtheorangeguy/adsb-monitoring/blob/HEAD/dashboards/adsb-aircraft-viewer.json). Refresh: `10s`.

<!-- Screenshot: after adding adsb-aircraft-viewer.png to .github/icons/adsb-monitoring/, replace this comment with ![ADS-B Aircraft Viewer](https://raw.githubusercontent.com/willtheorangeguy/.github/main/icons/adsb-monitoring/adsb-aircraft-viewer.png). -->

### Panels

| Panel | Type | What it shows |
| --- | --- | --- |
| Current Flights | geomap | See the query reference below. |
| Aircraft in View | stat | See the query reference below. |
| Aircraft with Position | stat | See the query reference below. |
| Receiver Messages / min | stat | See the query reference below. |
| Snapshot Age | stat | Age of the last Prometheus aircraft snapshot, not the age of a particular aircraft position. |
| Current Flight Details | table | Live aircraft rows; aircraft without a recent position remain in the receiver count but not this table. |
| Aircraft with Callsign | stat | Aircraft in the current receiver snapshot that advertise a flight callsign. |
| Emergency Squawk 7700 | stat | Aircraft currently reporting squawk 7700; zero is shown only while the aircraft scrape is healthy. |

<!-- Screenshot: add a focused panel or section image here after uploading it to .github/icons/adsb-monitoring/. -->

### Reading the results

The map may work while the Prometheus probes fail, or vice versa. Feeder active state does not prove remote sites accepted data. The feeder dashboard adapts Grafana.com dashboard 18398; retain attribution.

### Query reference

These expressions are copied from the dashboard JSON. Grafana substitutes the dashboard variables at runtime.

#### Current Flights

```promql
${aircraft_json_url}
```

#### Aircraft in View

```promql
count(adsb_aircraft_in_view{job="${job_adsb_receiver_aircraft}"}) or on() (0 * (up{job="${job_adsb_receiver_aircraft}"} == 1))
```

#### Aircraft with Position

```promql
count(adsb_aircraft_position_available{job="${job_adsb_receiver_aircraft}"}) or on() (0 * (up{job="${job_adsb_receiver_aircraft}"} == 1))
```

#### Receiver Messages / min

```promql
adsb_messages_last1m{job="${job_adsb_receiver_stats}"}
```

#### Snapshot Age

```promql
time() - adsb_aircraft_snapshot_seconds{job="${job_adsb_receiver_aircraft}"}
```

#### Current Flight Details

```promql
${aircraft_json_url}
```

#### Aircraft with Callsign

```promql
count(adsb_aircraft_callsign_available{job="${job_adsb_receiver_aircraft}"}) or on() (0 * (up{job="${job_adsb_receiver_aircraft}"} == 1))
```

#### Emergency Squawk 7700

```promql
count(adsb_aircraft_emergency_7700_active{job="${job_adsb_receiver_aircraft}"}) or on() (0 * (up{job="${job_adsb_receiver_aircraft}"} == 1))
```

## ADS-B Feeder & Receiver Stats

Source: [`dashboards/adsb-feeder-stats.json`](https://github.com/willtheorangeguy/adsb-monitoring/blob/HEAD/dashboards/adsb-feeder-stats.json). Refresh: `30s`.

<!-- Screenshot: after adding adsb-feeder-stats.png to .github/icons/adsb-monitoring/, replace this comment with ![ADS-B Feeder & Receiver Stats](https://raw.githubusercontent.com/willtheorangeguy/.github/main/icons/adsb-monitoring/adsb-feeder-stats.png). -->

### Panels

| Panel | Type | What it shows |
| --- | --- | --- |
| Aircraft in View | stat | See the query reference below. |
| Aircraft with Position | stat | See the query reference below. |
| Messages / second | stat | Completed decoder window, normalized by its actual duration. |
| Tracks / min | stat | See the query reference below. |
| Signal / Noise | stat | Mean signal and noise level over the completed decoder window; these are dBFS values, not an independently calculated SNR. |
| Receiver Gain | stat | See the query reference below. |
| Aircraft Counts | timeseries | See the query reference below. |
| Message & Track Rate | timeseries | See the query reference below. |
| Signal, Noise & Peak | timeseries | See the query reference below. |
| Position Decode Outcomes | timeseries | CPR decodes in the completed minute; not guaranteed positions delivered to feeder sites. |
| Decoder Input Quality | timeseries | See the query reference below. |
| Sample Drops & Strong Signals | timeseries | See the query reference below. |
| Receiver Gain & Changes | timeseries | See the query reference below. |
| Decoder CPU Time | timeseries | dump1090-fa per-window CPU milliseconds, not LXC CPU utilization. |
| Track Reliability | timeseries | See the query reference below. |
| Cumulative Decoder Messages | timeseries | See the query reference below. |
| Feeder & MLAT Services | stat | Systemd active state only. Active does not prove a remote feeding site accepted data. |

<!-- Screenshot: add a focused panel or section image here after uploading it to .github/icons/adsb-monitoring/. -->

### Reading the results

The map may work while the Prometheus probes fail, or vice versa. Feeder active state does not prove remote sites accepted data. The feeder dashboard adapts Grafana.com dashboard 18398; retain attribution.

### Query reference

These expressions are copied from the dashboard JSON. Grafana substitutes the dashboard variables at runtime.

#### Aircraft in View

```promql
count(adsb_aircraft_in_view{job="${job_adsb_receiver_aircraft}"}) or on() (0 * (up{job="${job_adsb_receiver_aircraft}"} == 1))
```

#### Aircraft with Position

```promql
count(adsb_aircraft_position_available{job="${job_adsb_receiver_aircraft}"}) or on() (0 * (up{job="${job_adsb_receiver_aircraft}"} == 1))
```

#### Messages / second

```promql
adsb_messages_last1m / (adsb_stats_window_end_seconds - adsb_stats_window_start_seconds)
```

#### Tracks / min

```promql
adsb_tracks_last1m
```

#### Signal / Noise

```promql
adsb_signal_dbfs
adsb_noise_dbfs
```

#### Receiver Gain

```promql
adsb_receiver_gain_db
```

#### Aircraft Counts

```promql
count(adsb_aircraft_in_view{job="${job_adsb_receiver_aircraft}"}) or on() (0 * (up{job="${job_adsb_receiver_aircraft}"} == 1))
count(adsb_aircraft_position_available{job="${job_adsb_receiver_aircraft}"}) or on() (0 * (up{job="${job_adsb_receiver_aircraft}"} == 1))
```

#### Message & Track Rate

```promql
adsb_messages_last1m / (adsb_stats_window_end_seconds - adsb_stats_window_start_seconds)
adsb_tracks_last1m / (adsb_stats_window_end_seconds - adsb_stats_window_start_seconds)
```

#### Signal, Noise & Peak

```promql
adsb_signal_dbfs
adsb_noise_dbfs
adsb_peak_signal_dbfs
```

#### Position Decode Outcomes

```promql
adsb_cpr_global_ok_last1m
adsb_cpr_local_ok_last1m
adsb_cpr_global_bad_last1m
adsb_cpr_global_range_last1m + adsb_cpr_global_speed_last1m + adsb_cpr_local_range_last1m + adsb_cpr_local_speed_last1m
```

#### Decoder Input Quality

```promql
adsb_local_accepted_zero_bit_last1m
adsb_local_accepted_one_bit_last1m
adsb_local_bad_last1m
adsb_local_unknown_icao_last1m
```

#### Sample Drops & Strong Signals

```promql
adsb_samples_dropped_last1m
adsb_strong_signals_last1m
```

#### Receiver Gain & Changes

```promql
adsb_receiver_gain_db
adsb_adaptive_gain_changes_last1m
```

#### Decoder CPU Time

```promql
adsb_decoder_cpu_demod_ms_last1m
adsb_decoder_cpu_reader_ms_last1m
adsb_decoder_cpu_background_ms_last1m
```

#### Track Reliability

```promql
adsb_tracks_last1m
adsb_tracks_single_message_last1m
adsb_tracks_unreliable_last1m
```

#### Cumulative Decoder Messages

```promql
adsb_receiver_messages_total
```

#### Feeder & MLAT Services

```promql
node_systemd_unit_state{instance="$feeder_instance",state="active",name=~"$feeder_unit_regex"}
```
