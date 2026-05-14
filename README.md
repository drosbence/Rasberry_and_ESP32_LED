# Raspberry Pi + ESP32 LED Timeline Sync

This project synchronizes a fullscreen video running on a Raspberry Pi with a WS2812B addressable LED strip controlled by an ESP32 over USB serial communication.

The installation creates a physical “timeline” effect: while the video plays, two soft white LED light islands start from both ends of the LED strip and move symmetrically toward the center. When the video loops, the LED animation resets to the beginning.

## Hardware

- Raspberry Pi 4
- Pimoroni HyperPixel 4.0 Square display, 720 × 720 px
- ESP32 development board
- WS2812B addressable LED strip
- USB cable between Raspberry Pi and ESP32

## System Architecture

The project has two parts:

### Raspberry Pi

The Raspberry Pi Python script:

- plays a fullscreen video using VLC embedded in a Tkinter window,
- reads the current VLC playback time,
- converts video progress into a timeline position,
- sends the position to the ESP32 over USB serial.

### ESP32

The ESP32 firmware:

- receives the timeline position over serial,
- drives the WS2812B LED strip using FastLED,
- creates two symmetrical moving 3-pixel white light islands,
- uses soft dimming for smoother movement.

## LED Configuration

The final working LED strip length is:

```cpp
#define TOTAL_LEDS 118
