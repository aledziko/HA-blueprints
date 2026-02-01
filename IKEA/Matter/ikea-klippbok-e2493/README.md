# 💧 IKEA KLIPPBOK E2493 Leak Sensor (Matter)

Full-featured automation for the **IKEA KLIPPBOK E2493** Matter leak sensor. This blueprint provides a highly flexible way to respond to leak detections, with support for immediate alerts, delayed secondary actions (if still wet), all-clear notifications, and integrated battery monitoring.

[![Import Blueprint to My Home Assistant](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Faledziko%2FHA-blueprints%2Fblob%2Fmain%2FIKEA%2FMatter%2Fikea-klippbok-e2493%2Fikea-klippbok-e2493-matter-leak-sensor.yaml)

### 🛠️ Manual Import URL
If the button above doesn't work, you can copy the URL below and paste it into the "Import Blueprint" dialog in Home Assistant:
`https://github.com/aledziko/HA-blueprints/blob/main/IKEA/Matter/ikea-klippbok-e2493/ikea-klippbok-e2493-matter-leak-sensor.yaml`

## 🌟 Key Features

*   **Dual-Stage Wet Actions**: Trigger something immediately (like a siren) and something else if it stays wet for a while (like a push notification).
*   **Dual-Stage Dry Actions**: Trigger actions as soon as it's dry, and optionally wait to confirm it stays dry.
*   **Integrated Battery Monitoring**: No need for separate battery automations. Get notified directly when the battery drops below your chosen threshold.
*   **Active Hours**: Restrict automation triggers to a specific time window (e.g., only during the day).
*   **Parallel Execution**: Uses Home Assistant's `parallel` mode to ensure multiple events (leak + low battery) are handled concurrently without missing a beat.
*   **Professional Logic**: Includes safety checks to ensure delayed actions only run if the sensor is still in the expected state.

## 💡 Example Use Cases

*   **🚨 Critical Alerts**: 
    *   **Wet Immediate**: Trigger a siren and flash red lights as soon as a leak is detected under the washing machine.
    *   **Wet Long**: If the sensor stays wet for 5 minutes, send a high-priority notification to all family members.
*   **🔌 Automatic Shutdown**: 
    *   **Wet Immediate**: Use a smart plug to instantly turn off the power to a dishwasher or water heater when moisture is sensed.
*   **✅ All Clear**: 
    *   **Dry Long**: Once the area has been dried, wait for 10 minutes to confirm it's truly clear before resetting your smart home's "Water Leak" status.
*   **🔋 Maintenance**: 
    *   **Battery Low**: Receive a notification when the battery level drops below 30%, giving you plenty of time to recharge or swap.

## 🛠️ Requirements

*   **IKEA KLIPPBOK (E2493)** sensor connected via **Matter**.
*   The sensor should expose a `binary_sensor` with `device_class: moisture`.
*   (Optional) The sensor should expose a `sensor` with `device_class: battery`.

## 📝 Attribution
This blueprint was inspired by the work of [censay](https://community.home-assistant.io/t/ikea-klippbok-matter-over-thread-leak-detector-e2493/968818) on the Home Assistant Community. This version expands on the original concept by adding integrated battery alerts, flexible action selectors, and advanced timing logic.

## 📄 License
Licensed under the **MIT License**.

---
### 🔗 More Blueprints & Community
Check out my other blueprints for IKEA Matter devices on the Home Assistant Community:

[**👉 Explore all my blueprints on the HA Forum**](https://community.home-assistant.io/search?q=@aledziko%20#blueprints-exchange)
