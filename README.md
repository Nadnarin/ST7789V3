# ST7789V3
ST7789V3 ESP32 show PNG

## Wiring
ST7789V3 → ESP32
- `Vcc`         → 3.3V
- `GND`         → GND
- `SCL / SCK`   → 18        Clock  SPI
- `SDA / MOSI`  → 23        Data 
- `DC`          → 4         Mode Data/Command
- `RES`         → 2         Reset 
- `CS`          → 15        Chip Select 
- `BLK`         → 5V        Backlight 


## Start png to Output header file (.h)
```py
png_path = "your_image_240x280.png"    # Source PNG image file
out_header = "my_image_240x280.h"      # Output header file (.h)
sym_name = "myImage240x280"            # Symbol name for the array in C
W, H = 240, 280                        # Target dimensions for the display
```
1. Set name PNG file from your image
2. Run in `cmd` pip install pillow
3. Set your address by `cd`
4. python `png_to_rgb565_header.py`
5. A file `my_image_240x280.h` will be created.
6. copy file `my_image_240x280.h` same folder `display.ino`
7. upload `display.ino`

## Result
![Demo Screenshot](1.png)
![Demo Screenshot](2.png)

