# Filter Ex — Extended Filter Sensor for Home Assistant

**Filter Ex** is a modified and backward-compatible version of the built-in `filter` integration.  
It fixes critical issues and extends functionality for time-based filtering.

---

## 🧩 Key Fixes and Improvements

### ✅ Startup Behavior
- Fixes the issue where the filtered sensor remained `unknown` after Home Assistant restart until the source entity updated.  
- The previous filtered value is now restored immediately after startup.

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
2. Search for **Filter Ex** and install it.  
3. Restart Home Assistant.

---

## 🧾 Example Configuration

```yaml
sensor:
  - platform: filter_ex
    name: "EXP Temp filtered ex"
    entity_id: sensor.exp_temp_source
    filters:
      - filter: time_simple_moving_average
        window_size: "01:00"
        precision: 2
        max_sub_interval: "00:10:00"
