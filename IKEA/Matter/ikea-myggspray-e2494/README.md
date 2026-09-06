# 🏃 IKEA MYGGSPRAY E2494 Motion Sensor (Matter)

Full-featured automation for the **IKEA MYGGSPRAY E2494** Matter motion sensor. This blueprint provides a highly flexible way to automate motion-based events, with integrated support for illuminance (LUX), sunlight-aware actions, and battery monitoring.

[![Import Blueprint to My Home Assistant](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Faledziko%2FHA-blueprints%2Fblob%2Fmain%2FIKEA%2FMatter%2Fikea-myggspray-e2494%2Fikea-myggspray-e2494-matter-motion-sensor.yaml)

### 🛠️ Manual Import URL
If the button above doesn't work, you can copy the URL below and paste it into the "Import Blueprint" dialog in Home Assistant:
`https://github.com/aledziko/HA-blueprints/blob/main/IKEA/Matter/ikea-myggspray-e2494/ikea-myggspray-e2494-matter-motion-sensor.yaml`

## 🌟 Key Features

*   **Flexible Action Selection**: Choose any Home Assistant action for both "Motion Detected" and "Motion Stopped".
*   **Smart Manual Override & Automation Latch**: Automatically distinguishes between manual turn-on (e.g. wall switch) and motion turn-on. If a light was already turned on manually, the blueprint will NOT shut it off when motion stops.
*   **Illuminance Cutoff**: Only trigger the "Motion Detected" action if the light level is below your chosen LUX threshold.
*   **Sunlight-Aware Actions**: Dedicated "High" and "Low" light thresholds to trigger actions when it gets too bright or too dark (e.g., closing/opening curtains).
*   **Integrated Battery Alerts**: Configurable low-battery monitoring (default 10%).
*   **Active Hours**: Restrict automation triggers to a specific time window (e.g., only during the night).
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

## 🛡️ Smart Manual Override & Automation Latch

Normally, motion automations shut off lights even if you manually turned them on (e.g., while working or taking a shower). **Smart Manual Override** solves this automatically:

* **Automatic Ownership**: If the light is `OFF` when motion starts, the blueprint turns the light on and sets the helper to `ON` (*"Automation owns this session"*). When motion stops, it safely turns the light off and resets the helper.
* **Manual Turn-On Protection**: If the light was already `ON` before motion was detected (e.g., turned on via a physical wall switch or app), the blueprint assumes manual control. When motion stops, it will **NOT** turn off the light!

### How to Enable:
1. **Create a Helper**: Go to **Settings -> Devices & Services -> Helpers**, click **+ Create Helper** -> choose **Toggle** (`input_boolean`). Give it a name like `Living Room Motion Latch`.
2. **In the Blueprint Settings**:
   * **Monitored Light / Switch**: Select the light or switch entity that this automation controls.
   * **Automation Latch Helper**: Select the Toggle helper you created above.
3. **Save**: The automation now automatically prevents unwanted shutoffs whenever lights are manually turned on!

---

## ⚠️ Troubleshooting

### 💡 Lux Sensor "Ignoring" Threshold?
If your lights turn on during the day even with a low cutoff, check the following:
*   **Stale Data**: IKEA Matter sensors are battery-powered and report motion *before* they report the light level (measured at ~1s lag). I've added a **1.5s delay** in v2.1 to ensure we catch the fresh value.
*   **Sensor Stuck**: Many IKEA sensors (E2494) have a hardware limitation where the lux reading can get "stuck" at a fixed value (often 1.0 lx) for long periods. If your Home Assistant entity shows 1.0 lx during the day, the blueprint will fire because it thinks it's dark!
*   **Re-Wake**: Try removing and re-inserting the battery to "wake" a stuck lux sensor, or check for firmware updates via the IKEA Home Smart app.

### 🔗 More Blueprints & Community
Check out my other blueprints for IKEA Matter devices on the Home Assistant Community:

[**👉 Explore all my blueprints on the HA Forum**](https://community.home-assistant.io/search?q=@aledziko%20#blueprints-exchange)
