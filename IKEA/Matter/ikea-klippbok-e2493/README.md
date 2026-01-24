# 💧 IKEA KLIPPBOK E2493 Leak Sensor (Matter)

Full-featured automation for the **IKEA KLIPPBOK E2493** Matter leak sensor. This blueprint provides a highly flexible way to respond to leak detections, with support for immediate alerts, delayed secondary actions (if still wet), all-clear notifications, and integrated battery monitoring.

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badget/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Faledziko%2FHA-blueprints%2Fblob%2Fmain%2FIKEA%2FMatter%2Fikea-klippbok-e2493%2Fikea-klippbok-e2493-matter-leak-sensor.yaml)

## 🌟 Key Features

*   **Dual-Stage Wet Actions**: Trigger something immediately (like a siren) and something else if it stays wet for a while (like a push notification).
*   **Dual-Stage Dry Actions**: Trigger actions as soon as it's dry, and optionally wait to confirm it stays dry.
*   **Integrated Battery Monitoring**: No need for separate battery automations. Get notified directly when the battery drops below your chosen threshold.
*   **Parallel Execution**: Uses Home Assistant's `parallel` mode to ensure multiple events (leak + low battery) are handled concurrently without missing a beat.
*   **Professional Logic**: Includes safety checks to ensure delayed actions only run if the sensor is still in the expected state.

## 🛠️ Requirements

*   **IKEA KLIPPBOK (E2493)** sensor connected via **Matter**.
*   The sensor should expose a `binary_sensor` with `device_class: moisture`.
*   (Optional) The sensor should expose a `sensor` with `device_class: battery`.

## 📝 Attribution

This blueprint was inspired by the work of [censay](https://community.home-assistant.io/t/ikea-klippbok-matter-over-thread-leak-detector-e2493/968818) on the Home Assistant Community. This version expands on the original concept by adding integrated battery alerts, flexible action selectors, and advanced timing logic.

## 📄 License

Licensed under the [MIT License](https://github.com/aledziko/HA-blueprints/blob/main/LICENSE).

---
### 🔗 More Blueprints
Check out my other blueprints for IKEA Matter devices:
*   [IKEA MYGGSPRAY Motion Sensor](https://github.com/aledziko/HA-blueprints/blob/main/IKEA/Matter/ikea-myggspray-e2494/ikea-myggspray-e2494-matter-motion-sensor.yaml)
*   [IKEA MYGGBETT Door/Window Sensor](https://github.com/aledziko/HA-blueprints/blob/main/IKEA/Matter/ikea-myggbett-e2492/ikea-myggbett-e2492-matter-door-sensor.yaml)

[Explore all my blueprints on the HA Forum](https://community.home-assistant.io/search?q=aledziko%20%23blueprints-exchange)
