# Changelog

All notable changes to this project will be documented in this file.

## 1.0.1 - Hook script
- Added selector for hook script: This script will start on each gesture and receive all availible variables
- Added knob_id variable

## 1.0.0 — First public release

- Home Assistant blueprint for Zigbee2MQTT rotary knobs (Moes ZG-101ZD & similar)
- Gesture mapping engine:
  - single / double click
  - hold / hold-release
  - rotate left / rotate right
  - hold + rotate left / right
- Support for Command and Event operation modes
- Noise-filter window to suppress false “tail” events
- Debug mode with persistent notifications and log output
- Customizable binding table for native Z2M events
- Optional helper variables available for scripts (gesture, rate, step_size, etc.)
- MQTT-based shared state-storage sensor:
  - reusable across multiple devices
  - designed for future extensions and additional blueprints
- Full user documentation:
  - installation (HACS + manual)
  - usage guide with screenshots
  - troubleshooting & debugging section
  - example: passing parameters to scripts

