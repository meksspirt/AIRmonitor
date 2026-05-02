# Air Monitor

A Home Assistant and ESPHome-based indoor air quality station built around an ESP32-C6 and a set of environmental sensors.  
It combines gas, ventilation, climate, and comfort data into a single clean dashboard and a custom air-quality index.

## Features

- Real-time indoor air monitoring
- ENS160 air quality index and rating
- SCD40 CO₂ monitoring
- TVOC tracking
- Temperature, humidity, and pressure measurements
- Smart combined air-quality logic
- Home Assistant dashboard with Bubble Card and mini graphs
- ESPHome firmware for easy deployment and OTA updates

## Hardware

Typical sensor stack:

- ESP32-C6 development board
- ENS160 air quality sensor
- SCD40 CO₂ sensor
- AHT20 temperature and humidity sensor
- BMP280 pressure sensor

Optional additions:

- PM2.5 sensor such as SPS30 or PMS7003
- Dedicated CO sensor
- VOC/NOx sensor module
- Display module for local UI

## How it works

The station reads environmental data from the sensors and sends them to Home Assistant through ESPHome.  
A custom air-quality score can be computed from ENS160 and CO₂ values to represent the current room state more realistically.

Core logic:

- ENS160 reflects air chemistry and general air quality
- SCD40 reflects ventilation and room freshness
- Temperature and humidity are used for compensation and context
- The final score can be used for dashboard color states, alerts, and automation

## Dashboard

The Home Assistant dashboard is designed to look like a clean AirVisual or PurpleAir style interface.

It can include:

- Main air quality card
- CO₂ card
- TVOC card
- Climate cards
- Graphs for trends
- Bubble Card popups for detailed views

## Installation

### 1. Flash ESPHome
Install ESPHome on the ESP32-C6 using your preferred method.

### 2. Add Wi-Fi credentials
Configure your Wi-Fi network and Home Assistant API key in the ESPHome YAML.

### 3. Connect the sensors
Wire the sensors according to their I2C or UART requirements.

### 4. Upload firmware
Compile and upload the firmware to the board.

### 5. Add the device to Home Assistant
Once the device is online, Home Assistant will discover the entities.

## Example ESPHome setup

```yaml
esphome:
  name: air-monitor
  friendly_name: Air Monitor

esp32:
  board: esp32-c6-devkitc-1
  framework:
    type: esp-idf

api:
ota:
wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

i2c:
  sda: GPIO20
  scl: GPIO19
  scan: true
