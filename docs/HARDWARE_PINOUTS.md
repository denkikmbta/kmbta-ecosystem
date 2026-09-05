# 🔌 KMBTA Hardware Cyberdeck — Pinout & Wiring Blueprint

## 1. Components
- **Microcontroller:** ESP32 Super Mini / ESP32-WROOM-32
- **IMU:** InvenSense MPU-6050 (6-DOF Gyroscope + Accelerometer)
- **Display:** 240x240 ST7789 Color TFT (SPI)
- **Touch Input:** XPT2046 Resistive Touch Controller (SPI)
- **Power:** 3.7V LiPo Battery + TP4056 USB-C Charging Module + Power Switch

---

## 2. Pin Mapping Table

| ESP32 Pin | Component Pin | Function / Protocol | Notes |
| :--- | :--- | :--- | :--- |
| **GPIO 21** | MPU-6050 SDA | I2C Data | 4.7kΩ Pull-up |
| **GPIO 22** | MPU-6050 SCL | I2C Clock | 4.7kΩ Pull-up |
| **GPIO 18** | ST7789 SCL / SCK | SPI Clock | Fast Hardware SPI |
| **GPIO 23** | ST7789 SDA / MOSI | SPI Data | Fast Hardware SPI |
| **GPIO 4** | ST7789 DC / RS | Data / Command | TFT Control |
| **GPIO 5** | ST7789 CS | Chip Select (Display) | Active Low |
| **GPIO 15** | ST7789 RST | Reset | Hardware Reset |
| **GPIO 2** | ST7789 BLK | Backlight PWM | Brightness dimming |
| **GPIO 25** | XPT2046 T_CLK | Touch SPI Clock | Shared or Soft SPI |
| **GPIO 32** | XPT2046 T_CS | Touch Chip Select | Active Low |
| **GPIO 33** | XPT2046 T_DIN | Touch MOSI | SPI Data In |
| **GPIO 27** | XPT2046 T_DO | Touch MISO | SPI Data Out |
| **GPIO 26** | XPT2046 T_IRQ | Touch Interrupt | Active Low touch event |
| **3.3V** | VCC (All) | Power Supply | Regulated 3.3V Rail |
| **GND** | GND (All) | Common Ground | System Ground |

---

## 3. Motion Axis Mapping
```
        [ Front / Nose of Cyberdeck ]
                    ▲
                    │
         (Yaw Z)    │    (Pitch X)
       ◄── 🔄 ──►   │      ▲  Tilt Up
       Left/Right   │      │
       (dx motion)  │      ▼  Tilt Down
                    │     (dy motion)
                    │
               [ MPU-6050 ]
                    │
                    ▼
          (Roll Y: Wrist Twist)
          Reserved for Flick Macros
```
