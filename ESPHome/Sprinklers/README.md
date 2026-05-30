# 💧 Smart Sprinkler System (ESPHome + Home Assistant)

A powerful, weather-aware irrigation system that supports independent scheduling, zone-level control, and automated hardware-level queuing.

[![Import Blueprint to My Home Assistant](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Faledziko%2FHA-blueprints%2Fblob%2Fmain%2FESPHome%2FSprinklers%2Fha-blueprint-sprinklers.yaml)

### 🛠️ Manual Import URL
If the button above doesn't work, you can copy the URL below and paste it into the "Import Blueprint" dialog in Home Assistant:
`https://github.com/aledziko/HA-blueprints/blob/main/ESPHome/Sprinklers/ha-blueprint-sprinklers.yaml`

## 🚀 Key Features

- **Zone Independence**: Set different schedules and durations for lawns, trees, or berry bushes using the same controller.
- **Hardware Queuing & Safety**: ESPHome handles the sequential activation of valves completely locally with safe delays (e.g., 40s), ensuring only one high-flow valve is open at a time.
  > [!NOTE]
  > **Why Queuing?** Manually toggling a valve switch in Home Assistant immediately aborts any active sequence for safety. Therefore, the blueprint strictly utilizes three custom ESPHome API services: `clear_queued_valves`, `queue_valve`, and `start_from_queue` to run sequences safely without network lag or conflicts.
- **Flexible Scheduling**:
  - **Weekdays Mode**: Choose specific days of the week (e.g., Mon, Wed, Fri for Lawns; Tue, Thu, Sat for Fruits).
  - **Interval Mode**: Run every N days (e.g., exactly every 3 days).
- **Weather-Responsive**: Automatically skips irrigation based on:
  - Local soil moisture sensors (e.g., EcoWitt WH51).
  - Current physical precipitation (rain gauge).
  - Daily weather forecasts (using the modern Home Assistant `weather.get_forecasts` API).
- **Smart Scaling Multiplier**: All ESPHome valves are configured with a base duration of **10 minutes**. The blueprint automatically converts the duration set in Home Assistant (e.g., 45 minutes) into the correct multiplier (e.g., `4.5` sent to the controller), offering high resolution and flexibility.
- **Manual Overrides**:
  - **Skip Next Run**: Easily skip the upcoming cycle via a wether-aware toggle. The blueprint automatically resets the toggle back to **OFF** once skipped, so you never have to remember to re-enable it!
  - **Winter Blowout**: Designed for easy winterization. It runs repeated short bursts (15s) across all zones for multiple cycles to help an air compressor purge the entire system of water.
  - **Test Mode**: Runs all zones for exactly 1 minute each to check for leaks or clogged heads.
- **Dynamic Status**: Real-time status sensor showing the active zone name and a **live countdown timer** (MM:SS) directly in your Home Assistant dashboard.
- **Advanced Safety & Access**:
  - **Local Web Server**: Access and control valves directly via the device's IP address in a web browser, even if Home Assistant or your network is offline.
  - **Restore Modes**: All physical valve relays are guaranteed to stay **OFF** after a power failure or device reboot.
  - **Emergency Shutdown**: Built-in cron-like time trigger to shut down all valves every morning at 6:00 AM.
  - **Notification Support**: Integrates with standard Home Assistant Action selectors to trigger push notifications or announcements before starting.

---

## 🛠️ Hardware Requirements

- **Microcontroller**: Recommended **WT32-ETH01** (ESP32 with built-in Ethernet) for maximum reliability, but compatible with any other ESPHome compatible board.
- **Relay Board**: Typically an 8-channel relay board, but the configuration is flexible—you can use more or fewer channels depending on your needs and available GPIOs.
- **Power Supply**: Appropriate for your valves (usually 24V AC) and the ESP32 (5V DC).

---

## 📦 Installation & Setup

### 1. ESPHome Configuration
1. Copy `esphome-sprinklers.yaml` and `secrets.yaml` to your ESPHome configuration directory.
2. Edit `secrets.yaml` and provide your own encryption keys and passwords.
3. Edit `esphome-sprinklers.yaml`:
   - Adjust the **board** and **connectivity** settings (WiFi example included).
   - Update the **GPIO pins** under `switch` to match your relay connections.
   - (Optional) Change zone names in the `text_sensor` lambda and `sprinkler` block.
4. Flash your device.

### 2. Home Assistant Blueprint
To automate the system with weather logic, use the provided Blueprint:

1. Import `ha-blueprint-sprinklers.yaml` into Home Assistant (**Settings > Automations > Blueprints**).
2. Create a new automation from the Blueprint.
3. Configure your **Schedule Mode**, selected zones, and weather/moisture sensors.

#### 🎛️ Setting up the "Skip Next Run" Helper (Rain Delay)
To utilize the smart, self-resetting skip switch:
1. Go to **Settings > Devices & Services > Helpers** (Ustawienia > Urządzenia oraz usługi > Pomocnicy) in Home Assistant.
2. Click **Create Helper** (Utwórz pomocnika) in the bottom right corner and select **Toggle** (Przełącznik).
3. Name it something descriptive (e.g., `Skip Next Irrigation` or `Pomiń następne podlewanie`) and click **Create**.
4. In your automation editor, assign this newly created helper entity to the **Skip Next Run (Optional)** input field.
5. Add this helper entity to your Dashboard (using an *Entities* or *Button* card) to have a convenient one-click manual skip toggle.
   > [!TIP]
   > The automation is fully self-managing: when triggered, if the toggle is ON, it will bypass the watering cycle, **automatically switch the toggle back to OFF** (to arm it for future schedules), and safely shut down.

#### 🌦️ How the Weather Forecast Logic Works
The blueprint leverages the modern Home Assistant 2024.4+ Service API to fetch weather and block irrigation before it rains:
1. **Fetching Daily Forecast**: The blueprint triggers the `weather.get_forecasts` service on your designated weather entity (e.g., `weather.dom` or `weather.home`) requesting a **daily** forecast type.
2. **Accessing Today's Data**: It parses the returned JSON payload and targets the first item (`forecasts[0]`), which represents the forecast for today.
3. **Evaluating Precipitation**: It reads the `precipitation` field (zapowiadane opady w mm). If today's forecasted rain is **greater than or equal to** your configured **Forecasted Rain Threshold** (e.g., `5 mm`), the run is aborted and skipped. If it's less (or 0), the automation proceeds.

> [!TIP]
> **Pro Tip for Different Zone Durations**: If some zones (e.g., vegetable garden) need more water than others (e.g., lawn), simply create **multiple automations** using the same Blueprint. This allows you to set independent schedules, durations, and weather thresholds for each group of zones.

---

## 📂 File Structure

- `esphome-sprinklers.yaml`: The main ESPHome configuration file.
- `secrets.yaml`: Placeholder for sensitive credentials.
- `ha-blueprint-sprinklers.yaml`: Home Assistant Blueprint for intelligent control.

---

## 🔧 Customization for Other Devices

This project is highly portable. If you are not using a WT32-ETH01:
1. Update the `board` and `platform` settings to match any other ESPHome compatible board.
2. Remove (or comment out) the `ethernet:` block and uncomment the `wifi:` section provided in the file.
3. Update the `pin:` numbers in the `switch:` section to match the available GPIOs on your device.

---

## 📄 License
This project is part of the [HA-blueprints](../../README.md) collection and is licensed under the MIT License.
