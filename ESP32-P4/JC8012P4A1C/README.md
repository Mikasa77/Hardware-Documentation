# Guition JC8012P4A1C

8" ESP32-P4 development board with MIPI DSI display, ESP32-C6 Wi-Fi co-processor, touch, camera, and audio.

## Quick reference

| | |
|---|---|
| SoC | ESP32-P4 rev v1.3, 360 MHz RISC-V |
| Display | 800×1280 portrait, MIPI DSI 2-lane, JD9365 driver IC |
| Memory | 16 MB QIO flash (Boya), 32 MB PSRAM @ 200 MHz |
| Co-processor | ESP32-C6 — 802.11 b/g/n + BLE 5 via ESP-Hosted SDIO |
| Touch | GSL3680, I2C GPIO 7/8, INT GPIO 21, RST GPIO 22 |
| Audio | ES8311 codec, I2S GPIO 9–13, power amp GPIO 20 |
| Camera | SC2336 2 MP, MIPI CSI-2 2-lane (not yet initialised) |
| IDF | v6.0.1 |

## Files

| File | Contents |
|---|---|
| [JC8012P4A1C.md](JC8012P4A1C.md) | Complete hardware reference — paste into agent context |

## Critical facts for new projects

- **Chip revision:** v1.3 (pre-v3 silicon). `sdkconfig.defaults` **must** include `CONFIG_ESP32P4_SELECTS_REV_LESS_V3=y` and `CONFIG_ESP32P4_REV_MIN_100=y` or esptool will refuse to flash.
- **PSRAM XIP:** Enabled. LVGL draw buffers must be `MALLOC_CAP_SPIRAM`. DMA2D can only read from PSRAM — internal SRAM as DMA source silently produces a blank display.
- **Cache coherency:** Call `esp_cache_msync(..., ESP_CACHE_MSYNC_FLAG_DIR_C2M | ESP_CACHE_MSYNC_FLAG_UNALIGNED)` before every `esp_lcd_panel_draw_bitmap()`.
- **C6 SDIO:** Slot 1, GPIO 14–19. Not Slot 0 (GPIO 39–44 — those are the TF card).
- **`swap_xy`:** Not supported by the JD9365 panel driver. Do not call it.
- **`sdkconfig` location:** Set `set(SDKCONFIG "${CMAKE_BINARY_DIR}/sdkconfig")` in `CMakeLists.txt` so `idf.py fullclean` always wipes it and forces regeneration from `sdkconfig.defaults`.

## Hardware validation status (2026-05-22)

| Subsystem | Status |
|---|---|
| Display (MIPI DSI, JD9365) | Confirmed |
| LVGL rendering | Confirmed |
| Audio (ES8311) | Confirmed |
| Wi-Fi SDIO transport (C6) | Confirmed |
| Touch init (GSL3680) | Confirmed — physical input not yet validated |
| Wi-Fi AP association | Not tested |
| TF card | Not tested |
| Camera (SC2336) | Not started |
| USB Serial/JTAG | Unknown |
