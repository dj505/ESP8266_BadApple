# ESP8266_BadApple
Bad Apple video by Touhou on ESP8266 with SSD1306 OLED, uses the Heatshrink compression library to decompress the RLE encoded video data.
First version, no sound yet, video only.

![Bad Apple on ESP32](ESP32_BadApple.jpg)

## Hardware Requirements
Runs on ESP8266 modules with OLED displays based on SSD1306. Typical modules are available from Heltec or TTGO or others.

## Software Requirements
* Arduino 1.8.x
* ESP8266 Arduino core from https://github.com/esp8266/Arduino/releases
* OLED display driver from https://github.com/ThingPulse/esp8266-oled-ssd1306
* ESP8266 SPIFFS Upload Plugin from https://github.com/esp8266/arduino-esp8266fs-plugin/releases

# Usage
* Adapt display pins in main sketch if necessary
* Upload sketch
* Upload sketch data via "Tools" -> "ESP8266 Sketch Data Upload"

Enjoy video. Pressing PRG button (GPIO0) for max display speed (mainly limited by I2C transfer), otherwise limited to 30 fps.

# How does it work
Video have been separated into >6500 single pictures, resized to 128x64 pixels using VLC. 
Python skript used to run-length encode the 8-bit-packed data using 0x55 and 0xAA as escape marker and putting all into one file.
RLE file has been further compressed using heatshrink compression for easy storage into SPIFFS (which can hold only 1MB by default). 
Heatshrink for Arduino uses ZIP-like algorithm and is available also as a library under https://github.com/p-v-o-s/Arduino-HScompression and 
original documentation is here: https://spin.atomicobject.com/2013/03/14/heatshrink-embedded-data-compression/

# Known issues
SPIFFS is broken currently (Feb 2018) in ESP32 Arduino core - hopefully will be fixed there soon. Search through issue list there for solutions - 
usually an earlier commit can be used to get it working. 


