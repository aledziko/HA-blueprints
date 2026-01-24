# 🌡️ IKEA TIMMERFLOTTE E2314 Temp/Humidity Sensor (Matter)

Pro-grade automation for the **IKEA TIMMERFLOTTE** Matter temperature and humidity sensor. This blueprint allows you to trigger specific actions when environmental levels cross your custom high or low thresholds.

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint URL pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Faledziko%2FHA-blueprints%2Fblob%2Fmain%2FIKEA%2FMatter%2Fikea-timmerflotte-e2314%2Fikea-timmerflotte-e2314-matter-temp-humidity-sensor.yaml)

## 🌟 Key Features

*   **Four Environmental Triggers**: Dedicated actions for High Temp, Low Temp, High Humidity, and Low Humidity.
*   **Custom Thresholds**: Easily set your desired numeric cutoffs for each state.
*   **Integrated Battery Monitoring**: Get notified when the sensor battery is low without needing extra automations.
*   **Parallel Execution**: Handles multiple environmental shifts concurrently.

## 💡 Example Use Cases

*   **🏢 HVAC Control**: 
    *   **High Temp**: Turn on your AC or ceiling fans when the room hits 26°C (79°F).
    *   **Low Temp**: Activate heating or a smart plug with a space heater when it drops below 18°C (64°F).
*   **🚿 Ventilation & Recuperation**:
    *   **High Humidity**: Automatically trigger the bathroom fan or a whole-home recuperation system when humidity spikes after a shower.
*   **🍷 Specialized Monitoring**:
    *   **Alerts**: Send push notifications if a wine cellar or greenhouse goes out of its ideal range.
*   **🔋 Maintenance**: 
    *   **Battery Low**: Receive a notification when the battery level drops below 30%, giving you plenty of time to recharge or swap.

## 🛠️ Requirements

*   **IKEA TIMMERFLOTTE** sensor connected via **Matter**.
*   Entities for **Temperature**, **Humidity**, and (optionally) **Battery**.

## 📄 License

Licensed under the **MIT License**.

---
### 🔗 More Blueprints & Community
Check out my other blueprints for IKEA Matter devices on the Home Assistant Community:

[**👉 Explore all my blueprints on the HA Forum**](https://community.home-assistant.io/search?q=aledziko%20%23blueprints-exchange)
