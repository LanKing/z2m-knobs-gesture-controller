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

This blueprint is better because it cleanly separates concerns:
- acts as a reusable **gesture-controller layer**
- normalizes raw MQTT events into clear gestures (single, double, hold, rotate…)
- handles Command/Event modes and noise filtering centrally
- exposes a clean action interface with optional helper variables

🎉 Your scripts stay small and focused on behavior, while the knob logic is configured once and reused everywhere.

## 🔧 Installation

### Easiest way — via HACS
> ℹ️ [What is HACS](#-appendix-1--what-is-hacs)?

1. Open **HACS → Blueprints**
2. Search for: `Z2M Knob — Gesture Action Controller`
3. Install the blueprint
4. Restart Home Assistant (please make full restart, not only automations reload. This needed because integration installs noise filter sensor to configuration)

## 🛍 Appendix 1 — What is HACS?

HACS (Home Assistant Community Store) is a community-driven extension system for Home Assistant.
It allows you to install third-party blueprints, integrations, dashboards, and custom components directly from GitHub — with update notifications and version management.

### How to install HACS

#### 🟢 The easiest way (Home Assistant OS / Supervised):
1. Go to **Settings → Add-ons → Add-on Store**
2. Search for **HACS**
3. Install the add-on and start it
4. Restart Home Assistant
5. Go to **Settings → Devices & Services → Add Integration → HACS**
6. Complete GitHub authorization:
> During the first-time setup, HACS will ask you to sign in to GitHub and authorize access.  
> You need a GitHub account for this (create one if needed: [https://github.com/signup](https://github.com/signup)).  
> 🧘‍♂️ The authorization is read-only — HACS can only download public repositories and cannot modify your GitHub account or data.  

#### 🟣 Alternative method (Docker / Core):
Follow the official manual install guide: [https://hacs.xyz/docs/use/download](https://hacs.xyz/docs/use/download)
