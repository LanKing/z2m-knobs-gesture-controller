🗺️ [How to use](#%EF%B8%8F-how-to-use) 🛠 [Installation](#-installation) 🐞 [Troubleshooting](#-troubleshooting)

# ⏲️ Z2M Knob — Gesture Action Controller (Moes ZG-101ZD & similar AliExpress-sold knobs)
Assign your actions to Zigbee2MQTT rotary-knob gestures in Home Assistant. Supports Command/Event modes and includes noise filtering for false “tail” events.

## ✨ Features
- Works with many Zigbee2MQTT rotary-knobs (brands such as Moes, Girier, and others — mostly AliExpress-sold models)
- Bind gestures to any HA actions or scripts, with optional helper parameters (gesture, step_size, rate, etc.)
- Supports both Command and Event operation modes (typically switched using a triple-click on most knobs)
- Noise filtering for accidental “tail” events (e.g., unwanted rotation after hold+rotate, or a single click triggered after rotation)
- Allows visual customization of native low-level events if your knob uses different payload values
- Supports configuring automation mode and maximum concurrent runs
- Debug output available via notifications or logs

## 💡 Why this blueprint is better than writing custom knob automations

Out of the box, Zigbee2MQTT rotary knobs only publish raw MQTT events.  
You *can* wire them directly into your automations — but that means:
- spending time inspecting and decoding raw MQTT payloads
- writing and maintaining custom automation logic
- duplicating the same mapping patterns across multiple automations
- mixing low-level device-handling code with your real logic (lights, scenes, etc.)
- debugging false “tail” events and edge-case behaviors

🎯 This blueprint is better because it turns raw MQTT events into clean, human-friendly gestures and lets you configure all actions through the UI — with zero YAML and zero custom automations. Instead of fighting payloads, you simply choose what each gesture does.

It also cleanly separates concerns:
- works as a reusable **gesture-controller layer** for any supported knob
- converts unpredictable MQTT events into consistent gestures (single, double, hold, rotate…)
- handles Command/Event modes and noise filtering automatically, in one place
- exposes a simple action interface with optional helper variables when you need more control

Your scripts stay small and focused on behavior, while the knob logic is configured once and reused everywhere.

## 🗺️ How to use

### Base usage

1. Create an automation from this blueprint in your Home Assistant: Settings → Automations & Scenes → Automations → Add Automation → Use Blueprint. Select: “Z2M Knob — Gesture Action Controller” from drop-down list.
2. Set the MQTT topic of your knob. Open Zigbee2MQTT → Devices → choose your knob → copy its Friendly name. Replace `your_knob_friendly_name` to copied value. Example: zigbee2mqtt/Bedroom_Knob. Now automation monitors events from your concrete knob.
3. Assign your actions to gestures (what each gesture will do). 

### Advanced usage

#### Debugging
Use Debug mode to test behavior. Set Debug = `notification`. A new notification will appear in HA. 
Open it, rotate and click the knob, and watch how gestures are mapped.

This helps you:
- see the **native event** coming from the device 
- verify whether an event was filtered as a “tail”  
- check the current **operation mode** (command/event)

If your knob produces different event values —  adjust them in the **gesture binding table** in the blueprint inputs.
If your knob uses a different operation-mode model — copy the debug payload and send it to me, I will add support.

#### Additional parameters for scripts
If you are advanced user and use scripts as actions, you can add parameters from automation.

## 🐞 Troubleshooting
- No actions trigger → enable Debug mode and check notifications/logs  
- Events look duplicated → increase noise filter window (ms)  
- Sensor unavailable → create the MQTT sensor and restart HA  
- Knob uses different payload values → adjust the binding table in inputs  



## 🛠 Installation

### ✨ Easiest way — via HACS
> ℹ️ [What is HACS?](#-appendix-1--what-is-hacs)

1. Open HACS and search for: `Z2M Knob — Gesture Action Controller`
3. Install it
4. Restart Home Assistant (please make full restart, not only automations reload. This needed because integration installs noise filter sensor to configuration)

### 👨‍💻 Manual way
1. Copy [those files](/CONFIG) to Home Assistant CONFIG directory
2. Ensure packages are enabled in CONFIG/configuration.yaml  
The following line (packages) is required. If it does not exist, add it:
```yaml
homeassistant:
  packages: !include_dir_named packages
```
3. Restart Home Assistant


## 📌 Compatibility
Tested primarily with:
- Moes ZG-101ZD  
- Zigbee2MQTT-compatible rotary knobs from Moes / Girier and similar brands  

Most similar Z2M knobs should work as long as their events can be mapped to gestures.


## 📄 License
MIT — contributions welcome.


## 🛍 Appendix 1 — What is HACS?

HACS (Home Assistant Community Store) is a community-driven extension system for Home Assistant.
It allows you to install third-party blueprints, integrations, dashboards, and custom components directly from GitHub — with update notifications and version management.

### How to install HACS

> During the first-time setup, HACS will ask you to sign in to GitHub and authorize access.  
> You need a GitHub account for this (create one if needed: [https://github.com/signup](https://github.com/signup)).  
> 🧘‍♂️ The authorization is read-only — HACS can only download public repositories and cannot modify your GitHub account or data.  

👉 [Follow the official HACS setup instruction](https://hacs.xyz/docs/use/#getting-started-with-hacs)

