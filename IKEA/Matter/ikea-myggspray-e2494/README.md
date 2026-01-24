# 🏃 IKEA MYGGSPRAY E2494 Motion Sensor (Matter)

Full-featured automation for the **IKEA MYGGSPRAY E2494** Matter motion sensor. This blueprint provides a highly flexible way to automate motion-based events, with integrated support for illuminance (LUX), sunlight-aware actions, and battery monitoring.

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint URL pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Faledziko%2FHA-blueprints%2Fblob%2Fmain%2FIKEA%2FMatter%2Fikea-myggspray-e2494%2Fikea-myggspray-e2494-matter-motion-sensor.yaml)

## 🌟 Key Features

*   **Flexible Action Selection**: Choose any Home Assistant action for both "Motion Detected" and "Motion Stopped".
*   **Illuminance Cutoff**: Only trigger the "Motion Detected" action if the light level is below your chosen LUX threshold.
*   **Sunlight-Aware Actions**: Dedicated "High" and "Low" light thresholds to trigger actions when it gets too bright or too dark (e.g., closing/opening curtains).
*   **Integrated Battery Alerts**: Configurable low-battery monitoring (default 10%).
*   **Parallel Mode**: Handles motion timers, light alerts, and battery checks concurrently.

## 💡 Example Use Cases

*   **🌙 Security & Comfort Lighting**: 
    *   **Motion Detected**: Turn on the porch light, but only if the illuminance is below 10 LUX (nighttime).
    *   **Motion Stopped**: Turn off the light after 2 minutes of inactivity.
*   **☀️ Smart Blinds & Curtains**: 
    *   **High Light**: Automatically close the smart blinds when the room gets too bright (e.g., above 5000 LUX) to prevent glare and overheating.
    *   **Low Light**: Open the blinds when the sun sets and the light level drops below your comfort threshold.
*   **🔋 Maintenance**: 
    *   **Battery Low**: Receive a notification when the battery level drops below 30%, giving you plenty of time to recharge or swap.

## 🛠️ Requirements

*   **IKEA MYGGSPRAY (E2494)** sensor connected via **Matter**.
*   The sensor should expose a `binary_sensor` with `device_class: motion` or `occupancy`.
*   (Optional) The sensor should expose sensors for `illuminance` and `battery`.

## 📄 License

Licensed under the **MIT License**.

---
### 🔗 More Blueprints & Community
Check out my other blueprints for IKEA Matter devices on the Home Assistant Community:

[**👉 Explore all my blueprints on the HA Forum**](https://community.home-assistant.io/search?q=aledziko%20%23blueprints-exchange)
