# ST7789V3
ST7789V3 ESP32 show PNG

## Wiring
ST7789V3 → ESP32
`Vcc`         → 3.3V

`GND`         → GND

`SCL / SCK`   → 18        Clock ของ SPI

`SDA / MOSI`  → 23        Data ส่งเข้า

`DC`          → 4         เลือกโหมด Data/Command

`RES`         → 2         Reset จอ

`CS`          → 15        Chip Select (บางโมดูลไม่มี, จะต่อ GND แทน)

`BLK`         → 5V         Backlight (ควบคุมไฟสว่าง)
