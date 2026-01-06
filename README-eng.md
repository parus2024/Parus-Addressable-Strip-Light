# Parus‑Addressable‑Strip‑Light: Parus Addressable Light Strip on ESPHome

![ESPHome Logo](images/esphome-icon.png)  ![Home Assistant Logo](https://avatars.githubusercontent.com/u/13844975?s=200&v=4)

<p align="center">
  <img alt="Static Badge" src="https://img.shields.io/badge/made%20by-ParusSmartHome-blue">
  <img alt="Static Badge" src="https://img.shields.io/badge/version-v1.0%20Beta-green">
  <img alt="Static Badge" src="https://img.shields.io/badge/esphome%20min%20version-2025.7.5-red">
  <img alt="Static Badge" src="https://img.shields.io/badge/license-MIT-orange">
</p>

## 🌟 Project Description

**Parus‑Addressable‑Strip‑Light** — The system is based on an addressable LED strip (such as WS2812B, etc.) controlled by a microcontroller (ESP8266/ESP32). It is ideal for decorative lighting, space zoning, and ambiance creation. Supports strips such as WS2812B, SK6812, and similar models. The project allows you to:
- create complex dynamic lighting effects;
- set up presets and playlists with various trigger conditions;
- play existing effects in random order with customizable duration;
- configure lighting scenarios via a web interface or API.

## 🔑 Key Features

### Effects and Visualization
- **Variety of effects**: rainbow, waves, flicker, flame, fireworks, etc. (over 30 options).
- **Presets**: save ready-made color and animation configurations.
- **Playlists**: sequential playback of effects on a schedule.
- **Random Mode**: play effects in random order with adjustable duration.

### Control
- **Home Assistant**: full control via API (color, brightness, effects).
- **Yandex Alice**: voice control (via Home Assistant).
- **Web page**: remote control via IP address.
- **API/MQTT**: integration with other systems.

## 🌟 Effects (List and Brief Description)

### Each effect is included via !include and is a separate YAML file with settings and logic. Below is a classification by type.

### 1. Holiday/Thematic:
- christmas_parus.yaml — Christmas palette (red, green, white), flickers and iridescence.
- candy_cane_parus.yaml — candy cane effect (red and white stripes).
- fireworks_parus.yaml — fireworks simulation (flashes, scattering sparks).

### 2. Natural/Animated:
- flames_vertical.yaml — vertical flame (smooth transitions of red, orange, yellow).
- lava_parus.yaml — lava effect (slow flows of orange-red hues).
- snow_flack_parus.yaml — falling snow (white sparks on a dark background).
- matrix_rain_parus.yaml — «matrix» rain (vertical streams of blue/white pixels).

### 3. Dynamic/Iridescent:
- rainbow_parus.yaml — rainbow (smooth movement across the color wheel).
- wave_parus.yaml, two_wave_parus.yaml — color waves (one or two moving bands).
- wheel_of_color_parus.yaml — rotating color wheel (spectrum moving along the strip).
- dynamic_smooth_parus.yaml — smooth transitions between specified colors.

### 4. Flickering/Sparkling:
- twinkle_parus.yaml — starry flicker (random bright dots).
- strobe_parus.yaml — strobe (sharp flashes of white/colored light).
- confetti_parus.yaml — confetti (many small colored «scraps»).
- explosion_parus.yaml — explosions (sharp expansions of bright spots).

### 5. Geometric/Structured:
- blue_scan_parus.yaml, bluez_parus.yaml — blue scanning lines or patterns.
- balls_parus.yaml — moving colored balls (spheres on the strip).
- trail_parus.yaml — trails (pixels leave «tails» when moving).
- tunnel_parus.yaml — tunnel effect (lines converging toward the center).

### 6. Minimalist/Background:
- breathing.yaml — breathing (smooth dimming and brightening).
- candle_parus.yaml — candle flame simulation (soft orange oscillations).
- noice_parus.yaml — noise (random pixels, like «snow» on a screen).
- sunrise_parus.yaml — sunrise (gradual brightening from red to white).

### 7. Others...

### Control: Presets and Playlists
The system supports presets (ready-made configurations) and playlists (sequential playback of effects), as shown in the repository example.

## Key Mechanisms:

### Presets: (save)
- the current effect;
- color, speed, intensity parameters;
- animation settings.
- Allow instant switching between scenarios (e.g., «Party», «Relaxation», «New Year»).

### Playlists
Define the order and duration of effect display.

### Random Playback
- Play effects in random order with adjustable duration.

### How to Expand the System
- Add effects: create a new YAML file in includes/strip_effects/ and include it in effects:.
- Adjust parameters: modify speed, colors, intensity in each effect.
- Create custom playlists: via YAML configuration or API.

## 🛠 Components and Hardware

### Main Components
- **Microcontroller**: ESP32/ESP8266 with at least 4 MB flash.
- **Addressable strip**: WS2812B and others.

### Software Dependencies
- **ESPHome**: version 2024+ (supports addressable strips and sensors).
- **Home Assistant**: integration via API.

## 📋 Installation and Configuration

### 1. Hardware Preparation
1. Connect the addressable strip to the microcontroller.
2. Install ESPHome on ESP32/ESP8266 with at least 4 MB flash (USB/OTA).
3. Connect power and test the strip’s functionality.

### 2. ESPHome Configuration
1. Open `parus_addressable_strip_light.yaml` in any editor or ESPHome Builder.
2. Configure `substitutions` for your setup (example):
```yaml
substitutions:
  name: parus-addressable-strip-light
  friendly_name: Parus Addressable Strip Light
  friendly_name_short: parus_addressable_strip_light
  version: '06.01.2025'
  device_ip: XXX.XXX.XXX.XXX
  reboot_timeout: 20min
  neopixel_pin: GPIO3
  neopixel_num_leds: 136
```
### 3. Required Components
Install required components explicitly or via references to necessary configuration files (example):

```yaml
<<: !include attach/common/esp/8266_nodemcuv2_restore.yaml
<<: !include attach/common/logger/debug.yaml
<<: !include attach/common/api.yaml
<<: !include attach/common/ota.yaml
<<: !include attach/common/wifi.yaml
```
### 4. Add necessary packages with correct paths (example ):
```yaml
packages:
  common: !include attach/packages/standart.yaml
  8266dma: !include attach/packages/neopixel_light_ws2812_8266dma.yaml
  playlist: !include attach/packages/strip_effect_preset_playlist.yaml
  random: !include attach/packages/strip_light_effect_random.yaml
```
to operate, you also need to link to  or explicitly specify them in the main file.

### 5. Home Assistant Integration

Add the device to Home Assistant.
## 🎮 Usage
Web Interface

Access via the device's IP address (when the web server component is activated).
Control: color, brightness, speed, and other effect parameters, presets.
Settings

- Color: Select color via palette.
- Brightness: Adjust brightness (0–100%).
- Effect: Choose an effect from the list.
- Preset: Load a saved effect configuration.
- Playlist: Set of effects for playback.
- Random Mode: Play effects in random order.

## 📊 Screenshots and Videos

- [Firmware YAML file](parus_addressable_strip_light.yaml)
- [Lighting example](images/addressable-fireworks-parus.jpg)
- [Web interface](images/interface_web.jpg)
- [HA interface](images/interface_ha.jpg)
- [YouTube overview](https://youtu.be/7ONLPmnGHnA)
- [Rutube overview](https://rutube.ru/video/f5aa4e9fea0d281e277900d629d03200/)

## Conclusion
The system combines a rich set of visual effects with flexible control via presets and playlists, making it ideal for decoration, holidays, and creating ambiance.

## 🙏 Acknowledgements

ESPHome community for the excellent framework.
Home Assistant for integration.
@andrewjswan for inspiration and ideas.
You for using it! If the project is useful, please star it on GitHub.

## 📄 License
This project is licensed under the MIT License — see the LICENSE file for details. Use at your own risk.

## Additional Resources

Telegram channel: https://t.me/parus_smart
