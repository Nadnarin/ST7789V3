#include <Arduino.h>
#include <SPI.h>
#include <pgmspace.h>           // For reading data from Flash (PROGMEM)
#include <Adafruit_GFX.h>       // Core graphics functions
#include <Adafruit_ST7789.h>    // ST7789 display driver

// ==== ESP32 SPI pins (VSPI) ====
#define TFT_MOSI 23   // VSPI MOSI
#define TFT_SCLK 18   // VSPI SCLK
#define TFT_CS   15   // Chip Select for the display
#define TFT_DC    2   // Data/Command
#define TFT_RST   4   // Display Reset

// Create ST7789 display object (works with Adafruit_GFX)
Adafruit_ST7789 tft(TFT_CS, TFT_DC, TFT_RST);

// Image file converted to RGB565 + PROGMEM (240x280)
#include "my_image_240x280.h"

// Draw RGB565 pixel block from PROGMEM onto the display in chunks (to save RAM)
static void drawRGB565FromPROGMEM(int16_t x, int16_t y, int16_t w, int16_t h,
                                  const uint16_t* progmem_pixels) {
  const size_t total = (size_t)w * h;   // Total pixels (240*280 = 67,200)
  const size_t CHUNK = 256;             // Send 256 pixels at a time (adjustable)
  uint16_t buf[CHUNK];                  // RAM buffer for each batch

  tft.startWrite();                     // Begin SPI transaction (faster)
  tft.setAddrWindow(x, y, w, h);        // Define drawing area on the display

  size_t sent = 0;
  while (sent < total) {
    size_t n = min(CHUNK, total - sent);
    // Read 16-bit pixels from Flash (PROGMEM) into RAM buffer
    for (size_t i = 0; i < n; ++i) {
      buf[i] = pgm_read_word(&progmem_pixels[sent + i]);
    }
    // Send buffer pixels to display (true = blocking until batch is done)
    tft.writePixels(buf, n, true);
    sent += n;
  }
  tft.endWrite();                       // End SPI transaction
}

void setup() {
  // Initialize SPI with custom pins (MISO not used, so set to -1)
  SPI.begin(TFT_SCLK, -1, TFT_MOSI, TFT_CS);

  // Initialize ST7789 display: 240x280 pixels (width x height)
  tft.init(240, 280);

  // 0 = portrait (0°). If the image is rotated, try 1, 2, or 3
  tft.setRotation(0);

  // Set SPI speed to 40 MHz (ESP32 can handle this with short wires/good soldering)
  tft.setSPISpeed(40000000);

  // Clear screen with black
  tft.fillScreen(ST77XX_BLACK);

  // Draw the full image from PROGMEM (MYIMG_W=240, MYIMG_H=280 must match the file)
  drawRGB565FromPROGMEM(0, 0, MYIMG_W, MYIMG_H, myImage240x280);
}

void loop() {
  // Do nothing further — image stays on screen
}
