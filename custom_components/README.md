# Filter Ex — Extended Filter Sensor for Home Assistant

Enhanced version of the built-in `filter` sensor with support for:
- Time-based moving averages (SMA, EMA)
- Unevenly spaced data (Eckner-style)
- Optional `max_sub_interval` for periodic forced updates

## Installation (via HACS)
1. Add this repository to HACS as a custom repository.
2. Search for “Filter Ex” and install it.
3. Restart Home Assistant.

## Example configuration

```yaml
sensor:
  - platform: filter_ex
    name: "Temperature filtered"
    entity_id: sensor.temperature_source
	max_sub_interval: "00:10:00"
    filters:
      - filter: time_simple_moving_average
        window_size: "01:00"
        precision: 2
        
