# Personal Home Assistant (Raspberry Pi 5)

A modular, local-first personal home assistant built around a Raspberry Pi 5.  
The system integrates computer vision, environmental sensing, voice interaction, and a local/remote UI for monitoring and control.

## Goals
- Provide a **single physical hub** with:
  - Object recognition via camera (AI vision)
  - Temperature & humidity sensing
  - Voice commands (microphones) and spoken responses (speaker)
  - Local display UI
- Offer a **secure remote dashboard** for out-of-home monitoring.
- Keep the architecture **modular** (separate services) and **easy to extend**.

## Hardware (Planned)
- Raspberry Pi 5 (main compute)
- Camera (CSI or USB)
- Temperature & humidity sensor (I2C; e.g., BME280 / SHT31)
- Microphones (USB or I2S mic array)
- Speaker / amplifier (USB / jack / I2S amp)
- Display (HDMI or DSI)
- 3D-printed enclosure/structure for rigid integration and clean cable routing
- Optional: AI accelerator (e.g., Coral USB / Hailo) and UPS HAT

## Main Features
### Environmental Monitoring
- Read temperature/humidity periodically
- Store and visualize historical trends
- Trigger automations/alerts based on thresholds

### Computer Vision
- Camera streaming (local)
- Object detection events (e.g., person, package, pet)
- Optional snapshots on events and notifications

### Voice Assistant
- Wake word or push-to-talk (MVP)
- Speech-to-text (ASR) → intent parsing → action
- Text-to-speech (TTS) responses through speakers

### UI & Remote Access
- Local dashboard on the attached screen (kiosk mode)
- Secure remote access (VPN or tunnel + HTTPS)
- Live device status + sensor charts + camera view + event history

## Architecture Overview
The project is split into services to keep development clean and testable:

- **device_service**: reads sensors, publishes telemetry
- **vision_service**: handles camera ingest + object detection, publishes events
- **voice_service**: ASR/NLU/TTS pipeline, publishes commands, receives responses
- **orchestrator**: automation logic and global state management
- **ui**: local/remote dashboard

Communication is event-driven:
- **MQTT** for telemetry/events/commands (lightweight IoT standard)
- Optional **REST/WebSocket** for richer interactions

## Repository Structure
```text
home-assistant-bot/
  docker/
    compose.yml
    mosquitto/
    reverse-proxy/
  services/
    device_service/
    voice_service/
    vision_service/
    orchestrator/
    ui/
  shared/
    schemas/
    common_lib/
  docs/
    architecture.md
    wiring.md
