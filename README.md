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

### IKEA MYGGSPRAY E2494 Motion Sensor (Matter)
- **Description**: Flexible action-based motion automation. Supports arbitrary actions for both motion detected and motion stopped events.
- **Protocol**: Matter over Thread
- **Key Features**: Trigger any action in HA, customizable wait time delay, and "restart" mode for high reliability.

## 🛠️ How to Import

To import these blueprints into your Home Assistant:

1. Go to **Settings > Automations & Scenes > Blueprints**.
2. Click **Import Blueprint** (bottom right).
3. Paste the **Raw URL** of the `.yaml` file from this repository.
4. Click **Preview** and then **Import**.

## 📄 License
This collection is shared with the community. Feel free to use and adapt these blueprints for your home automation needs.
