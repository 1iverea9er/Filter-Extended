# Extended Filter Sensor for Home Assistant

**Filter Ex** is a modified and backward-compatible version of the built-in [`filter`](https://www.home-assistant.io/integrations/filter) integration.  
It fixes [#154014](https://github.com/home-assistant/core/issues/154014#issuecomment-3388830668) and extends functionality for time-based filtering.

---

## 🧩 Key Fixes and Improvements

### 🕒 Time-Based Filter Reliability
- Correct handling of **time-dependent filters** (SMA, EMA) for **unevenly spaced data**, following *Eckner’s algorithm*.  
- Filters now properly converge to the source sensor value when the input stabilizes.

### 🔁 Forced Update Mechanism (`max_sub_interval`)
- Adds an **optional** configuration parameter for time-dependent filters.  
- Ensures regular forced updates even when the source value does not change, preventing stale output.  
- When omitted, behavior is **identical to the original integration**.

---

## ⚙️ Installation (via HACS)

1. Add this repository as a **custom repository** in HACS.  
2. Search for **filter (Extended)** and install it.  
3. Restart Home Assistant.

---

## 🧾 Example Configuration

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
