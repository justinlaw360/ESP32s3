# ESP32-S3-Touch-LCD-1.85C

https://www.waveshare.com/wiki/ESP32-S3-Touch-LCD-1.85
<img width="998" height="876" alt="image" src="https://github.com/user-attachments/assets/2a6468bc-79ee-4bf9-81dd-6fd8d7065b0b" />

https://www.waveshare.net/w/upload/2/25/ESP32-S3-Touch-LCD-1.85C--Schematic.pdf_.pdf

ESP32-S3-LCD-1.85 is a microcontroller development board with 2.4GHz WiFi and Bluetooth BLE 5 support, integrates high-capacity Flash and PSRAM. Onboard 1.85inch LCD display which can smoothly run GUI programs such as LVGL, optional for capacitive touch function. Combined with various peripheral interfaces, suitable for the quick development of the HMI and other ESP32-S3 applications.

* Equipped with high-performance Xtensa 32-bit LX7 dual-core processor, up to 240MHz main frequency
* Supports 2.4GHz Wi-Fi (802.11 b/g/n) and Bluetooth 5 (LE), with onboard antenna
* Built-in 512KB SRAM and 384KB ROM, with onboard 16MB Flash and 8MB PSRAM
* Onboard 1.85inch LCD display, 360×360 resolution, 262K color
* Optional for capacitive touch function controled via I2C interface, with interrupt support
* Adapting UART, I2C and some IO interfaces
* Onboard audio decoder, Microphone, QMI8658 6-axis sensor, RTC sensor, TF card slot and battery recharge management module, etc.
* Supports accurate control such as flexible clock and multiple power modes to realize low power consumption in different scenarios

Components Preparation
* ESP32-S3-Touch-LCD-1.85 x1
* TF card with MP3 files x1
* USB cable (Type-A to Type-C) x 1
* PCM5101 2030 speaker 8Ω 2w× 1
* MSM261S4030H0R microphone
* CST816 Touch driver
* ST77916 LCD
* QSPI connector

<img width="960" height="820" alt="image" src="https://github.com/user-attachments/assets/fe1c0e5e-50e9-4dbd-b596-0e521a59ed18" />

1. ESP32-S3R8
dual-core processor, up to 240MHz operating frequency
2. 16MB Flash
3. QST attitude sensor
4. QMI8658C (6-axis IMU includes a 3-axis gyroscope and a 3-axis accelerometer)
5. TCA9554PWR
6. GPIO expander chip
7. PCM5101 audio decoder
8. Amplifier chip
9. Battery recharge manager
10. ME6217C33M5G
11. Low dropout regulator, 800mA output (Max.)
12. RTC chip
13. PCF85063 RTC chip
14. Onboard ceramic antenna
15. IPEX1 connector
16. Switching to use external antenna via resoldering a onboard resistor
17. TF card slot
18. Speaker header
19. Comes with 8Ω 2W 2030 speaker
20. Volume adjustment knob
21. Microphone
22. UART header
23. Power indicator
24. USB Type-C port
25. RTC battery header for connecting rechargeable RTC battery
26. Charge indicator
27. Lithium battery charge indicator, lights up when charging, off when fully charged (the light status is uncertain when the battery is not connected)
28. I2C header connecting with internal chip, only supports the I2C peripherals and cannot be mapped to other functions

⚙️ Build Steps Overview


Install prerequisites
Shellsudo apt-get install git wget flex bison gperf python3 python3-pip python3-venv cmake ninja-build ccache libffi-dev libssl-dev dfu-util libusb-1.0-0Show more lines


Clone LVGL MicroPython repo
Shellgit clone https://github.com/lvgl-micropython/lvgl_micropython.gitcd lvgl_micropythongit submodule update --init --recursiveShow more lines


Set up ESP-IDF v5.x
Shellgit clone -b v5.4 --recursive https://github.com/espressif/esp-idf.gitcd esp-idf./install.shsource export.shShow more lines


Configure build for ESP32-S3 with PSRAM
Use make.py or idf.py with parameters like:
python3 make.py esp32 board=ESP32_GENERIC_S3 board_variant=SPIRAM_OCT flash-size=16 psram-size=16 display=ST77916 indev=CST816S



Flash firmware
esptool.py --chip esp32s3 erase_flashesptool.py --chip esp32s3 write_flash -z 0x0 build/firmware.binShow more lines



🖥 Display & Touch Integration

ST77916: Requires RGB or SPI interface configuration in lv_conf.h and LVGL driver setup.
CST816S: I²C-based touch driver; ensure correct pins and enable in lvgl_micropython/drivers/touch.




