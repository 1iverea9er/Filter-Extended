Filter Ex — Extended Filter Sensor for Home Assistant

Modified and backward-compatible version of the built-in filter integration.
Fixes critical behavioral limitations of the original component and extends its functionality.

Key Fixes and Improvements

Startup fix:
Resolves issue where the filtered sensor remained unknown after Home Assistant restart until new source updates arrived.
Filter Ex now restores its previous filtered value immediately after startup.

Time-based filter reliability:
Correct handling of time-dependent filters (SMA, EMA) based on unevenly spaced data following Eckner’s algorithm.
Filters now correctly converge to the source sensor when its value stabilizes.

Forced update mechanism (max_sub_interval):
Adds optional configuration parameter for time-based filters.
Ensures regular refresh of the filter output even when the source value remains constant, preventing stale states.
Omission of this parameter preserves the exact behavior of the original integration.

Installation (via HACS)

Add this repository as a custom repository in HACS.

Search for Filter Ex and install it.

Restart Home Assistant.

Example Configuration
sensor:
  - platform: filter_ex
    name: "EXP Temp filtered ex"
    entity_id: sensor.exp_temp_source
    filters:
      - filter: time_simple_moving_average
        window_size: "01:00"
        precision: 2
        max_sub_interval: "00:10:00"


When max_sub_interval is defined, the sensor performs a forced refresh every 10 minutes even if the source value remains unchanged.
If omitted, the integration behaves identically to the original filter platform.
