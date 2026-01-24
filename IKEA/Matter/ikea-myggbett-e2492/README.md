# 🚪 IKEA MYGGBETT E2492 Door/Window Sensor (Matter)

Full-featured automation for the **IKEA MYGGBETT E2492** Matter Door/Window Sensor. This blueprint supports multi-stage actions for both opened and closed states, allowing you to handle immediate responses and delayed "safeguard" or notification actions in a single automation.

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint URL pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Faledziko%2FHA-blueprints%2Fblob%2Fmain%2FIKEA%2FMatter%2Fikea-myggbett-e2492%2Fikea-myggbett-e2492-matter-door-sensor.yaml)

## 🚀 Benefits

*   **Multi-Stage Logic**: Trigger immediate actions (e.g., turn on light) followed by delayed actions (e.g., notify if door is left open too long).
*   **Parallel Execution**: Handles multiple state changes and timers concurrently.
*   **Battery Management**: Built-in battery low monitoring with a configurable threshold (default 30%).
*   **Highly Flexible**: All actions are optional and support multiple sub-actions.

## 💡 Example Use Cases

*   **Bathroom Occupancy**: 
    *   **Open**: Turn on light.
    *   **Closed Long**: After 30 minutes of being closed, ensure lights are off as a backup.
*   **Garage Door Security**:
    *   **Open Immediate**: Turn on garage light.
    *   **Open Long**: After 15 minutes, notify "Garage door left open!" or automatically close it.

## 🛠️ Requirements

*   **IKEA MYGGBETT (E2492)** sensor connected via **Matter**.
*   The sensor should expose a `binary_sensor` with `device_class: door`, `window`, or `opening`.
*   (Optional) The sensor should expose a `sensor` with `device_class: battery`.

## 📄 License

Licensed under the **MIT License**.

---
### 🔗 More Blueprints & Community
Check out my other blueprints for IKEA Matter devices on the Home Assistant Community:

[**👉 Explore all my blueprints on the HA Forum**](https://community.home-assistant.io/search?q=aledziko%20%23blueprints-exchange)
