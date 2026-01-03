# ⏲️ Z2M Knob — Gesture Action Controller (Moes ZG-101ZD & similar AliExpress-sold knobs)
Assign your actions to Zigbee2MQTT rotary-knob gestures in Home Assistant. Supports Command/Event modes and includes noise filtering for false “tail” events.

✨ Features
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

- decoding and tracking low-level events yourself
- mixing “knob driver / event parsing” logic with your real logic (lights, scenes, etc.)
- duplicating the same mapping code for every knob and every setup

This blueprint is better because it separates concerns:

- works as a reusable **gesture controller layer**
- normalizes raw MQTT events into clean gestures (single, double, hold, rotate…)
- handles Command/Event modes and noise filtering centrally
- exposes a clean action interface with optional helper variables

Your scripts stay small and focused on behavior,  
while the knob logic is configured once and reused everywhere.
