# 🌬️ IKEA ALPSTUGA E2495 Air Quality Sensor (Matter)

Pro-grade automation for the **IKEA ALPSTUGA E2495** Matter Air Quality sensor. This blueprint allows you to trigger specific actions when any environmental metric (CO2, PM2.5, Air Quality Index, Temperature, or Humidity) crosses your custom thresholds.

> [!NOTE]
> The **Air Quality** entity is a general "Air Quality Index" (AQI) calculated by the device (usually based on PM2.5 and CO2 levels). While the ALPSTUGA does not have a dedicated VOC sensor, this summary state is a great way to trigger whole-room air clear actions.

[![Import Blueprint to My Home Assistant](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Faledziko%2FHA-blueprints%2Fblob%2Fmain%2FIKEA%2FMatter%2Fikea-alpstuga-e2495%2Fikea-alpstuga-e2495-matter-air-quality-sensor.yaml)

### 🛠️ Manual Import URL
If the button above doesn't work, you can copy the URL below and paste it into the "Import Blueprint" dialog in Home Assistant:
`https://github.com/aledziko/HA-blueprints/blob/main/IKEA/Matter/ikea-alpstuga-e2495/ikea-alpstuga-e2495-matter-air-quality-sensor.yaml`

## 🌟 Key Features

*   **Five Environmental Triggers**: Dedicated actions for CO2, PM2.5, Air Quality summary, Temperature, and Humidity.
*   **Dual-Phase Actions**: Set numeric cutoffs (CO2, PM2.5, Temp, Humidity) or state lists (AQI Summary) for both "Alert" and "Normal" phases. This allows you to start and stop devices automatically as conditions change.
*   **Stabilization Time**: Prevent notification "flapping" by requiring states to remain active for a configurable duration (e.g., 30 seconds).
*   **Parallel Execution**: Handles multiple environmental shifts concurrently (e.g., boosting the air purifier while notifying about high CO2).
*   **Time Window Control**: Optional toggle to restrict the automation to specific hours (e.g., 8:00 AM - 10:00 PM), perfect for sleeping hours.

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

## 🛡️ Threshold Bind (Strict Cycle)

By default, Home Assistant automations are "stateless"—they don't easily remember what happened five minutes ago. If your humidity sensor fluctuates between 59.9% and 60.1%, you might get 10 notifications in a row.

**Threshold Bind** solves this by adding "Memory" to your automation. It ensures that once a "High" alert triggers, it is **locked**. It will not fire again until the sensor has safely returned to the "Low" (Safe) threshold first.

### How to Enable:
1.  **Create a Helper**: Inside the blueprint settings, find the **Threshold bind** input for your sensor (e.g., Humidity).
2.  **Toggle Button**: Click the dropdown and select **"Create new Toggle helper"**. 
3.  **Name it**: Give it a clear name like `Kitchen Humidity Bind`.
4.  **Save**: Once selected, the automation will now use this helper to "latch" the state and prevent notification storms.

> [!IMPORTANT]
> **Unique per Automation**: If you have two different automations (e.g., one for the Bedroom and one for the Office), you **MUST** create a unique helper for each. If they share the same helper, one room's humidity will "lock" the other room's alerts!

---
### ⚠️ Troubleshooting
**Preventing Repeated Actions?**
If you notice actions firing multiple times (e.g., your ventilation toggling on/off or receiving duplicate alerts) even when the air quality is stable, this blueprint has robust filtering built-in:
*   **Strict Logic**: Actions only trigger if the value actually **crosses** the threshold. If CO2 drops from 798 to 797 (both below the default 800 limit), the automation ignores it.
*   **Blip Filtering**: Brief "Unavailable" states from the sensor are automatically filtered out.
*   **Optimization**: Use the **Action Trigger Stabilization Time** (e.g., 30s) to further smooth out noisy data. This ensures your siren or fan doesn't toggle rapidly due to minor sensor fluctuations.

### 🔗 More Blueprints & Community
Check out my other blueprints for IKEA Matter devices on the Home Assistant Community:

[**👉 Explore all my blueprints on the HA Forum**](https://community.home-assistant.io/search?q=@aledziko%20#blueprints-exchange)
