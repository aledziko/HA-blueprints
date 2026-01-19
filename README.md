# HA-blueprints

This repository enables easy and flexible configuration for smart home device automation in Home Assistant. 

The goal of these blueprints is to make it possible to trigger **any action** in Home Assistant based on events from supported devices, providing maximum control without being locked into specific entities or services.

## 📂 Repository Structure

The blueprints are organized by manufacturer and protocol:

```text
HA-blueprints/
├── IKEA/
│   └── Matter/
│       └── ikea-myggspray-e2494/    # Motion Sensor
└── ... (future devices)
```

## 🚀 Blueprints Overview

### IKEA MYGGSPRAY E2494 Motion Sensor (Matter) v2.0
- **Description**: Pro-grade, multi-functional automation. Supports motion, illuminance (lux thresholds), and battery alerts.
- **Protocol**: Matter over Thread
- **Blueprint URL**: [Import Link](https://github.com/aledziko/HA-blueprints/blob/main/IKEA/Matter/ikea-myggspray-e2494/ikea-myggspray-e2494-matter-motion-sensor.yaml)
- **Key Features**: 
    - **Dynamic Motion**: Only triggers lights if below a LUX cutoff (optional, default 0).
    - **Sunlight Control**: Separate "High" and "Low" actions tuned for indoor ranges (0-3000 lx).
    - **Battery Alerts**: Get notified when sensor batteries run low.
    - **Parallel Mode**: High reliability—multiple sensors (motion, light, battery) never block each other.

## 🛠️ How to Import

To import these blueprints into your Home Assistant:

1. Go to **Settings > Automations & Scenes > Blueprints**.
2. Click **Import Blueprint** (bottom right).
3. Paste the **Blueprint URL** provided above.
4. Click **Preview** and then **Import**.

## 📄 License
This collection is shared with the community. Feel free to use and adapt these blueprints for your home automation needs.
