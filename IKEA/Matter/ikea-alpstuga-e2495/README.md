# 🌬️ IKEA ALPSTUGA E2495 Air Quality Sensor (Matter)

Pro-grade automation for the **IKEA ALPSTUGA E2495** Matter Air Quality sensor. This blueprint allows you to trigger specific actions when any environmental metric—CO2, PM2.5, Air Quality Index, Temperature, or Humidity—crosses your custom thresholds.

> [!NOTE]
> The **Air Quality** entity is a general "Air Quality Index" (AQI) calculated by the device (usually based on PM2.5 and CO2 levels). While the ALPSTUGA does not have a dedicated VOC sensor, this summary state is a great way to trigger whole-room air clear actions.

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint URL pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Faledziko%2FHA-blueprints%2Fblob%2Fmain%2FIKEA%2FMatter%2Fikea-alpstuga-e2495%2Fikea-alpstuga-e2495-matter-air-quality-sensor.yaml)

## 🌟 Key Features

*   **Five Environmental Triggers**: Dedicated actions for CO2, PM2.5, Air Quality summary, Temperature, and Humidity.
*   **Dual-Phase Actions**: Set numeric cutoffs (CO2, PM2.5, Temp, Humidity) or state lists (AQI Summary) for both "Alert" and "Normal" phases. This allows you to start and stop devices automatically as conditions change.
*   **Stabilization Time**: Prevent notification "flapping" by requiring states to remain active for a configurable duration (e.g., 30 seconds).
*   **Parallel Execution**: Handles multiple environmental shifts concurrently (e.g., boosting the air purifier while notifying about high CO2).

## 💡 Example Use Cases

*   **🍃 Air Purification**: 
    *   **Air Quality High**: Automatically boost your air purifier to "High" when the general air quality index drops.
    *   **PM2.5 High**: Trigger targeted actions for dust or smoke levels above 25 µg/m³.
*   **🛏️ Healthy Sleep & Focus**:
    *   **CO2 High**: Receive an alert or flash a light in your office or bedroom when CO2 levels exceed 1000 ppm, signaling it's time to open a window.
*   **🛁 Ventilation & Recuperation**:
    *   **High Humidity**: Automatically trigger the bathroom fan or a whole-home recuperation system when humidity levels spike.
*   **🏢 HVAC Control**: 
    *   **High Temp**: Turn on cooling when the room hits 26°C (79°F).
    *   **Low Temp**: Activate heating when it drops below 18°C (64°F).

---

### 💡 Pro Tip: Dynamic Notifications
You can make your alerts smarter by including the actual sensor value or state in your message. When setting up a notification action, use the following template in your message text:

*   **For CO2/PM2.5**: `CO2 level is now {{ trigger.to_state.state }} ppm`
*   **For Air Quality**: `Air quality status is now {{ trigger.to_state.state }}`

---

### 🛡️ Preventing "Notification Storms"
If you are receiving too many notifications in a short time, it's usually caused by the sensor "flapping" between states. To fix this:

1.  **Adjust Trigger States**: In the Air Quality settings, ensure you **unselect "Good" and "Fair"**. This prevents getting an alert every time the air *improves* back to normal.
2.  **Use Stabilization Time**: Increase the **Stabilization Time** (e.g., to 30 or 60 seconds). The blueprint will then wait for the sensor to stay at the new state for that duration before alerting you.

---

## 🛠️ Requirements

*   **IKEA ALPSTUGA (E2495)** sensor connected via **Matter**.
*   Entities for **CO2**, **PM2.5**, **Air Quality Index**, **Temperature**, and **Humidity**.

## 📄 License

Licensed under the **MIT License**.

---
### 🔗 More Blueprints & Community
Check out my other blueprints for IKEA Matter devices on the Home Assistant Community:

[**👉 Explore all my blueprints on the HA Forum**](https://community.home-assistant.io/search?q=aledziko%20%23blueprints-exchange)
