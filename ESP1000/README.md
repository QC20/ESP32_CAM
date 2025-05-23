> **Note**: This content is sourced from [https://w2.electrodragon.com/Board-dat/ESP/ESP1000-dat/ESP1000-dat.md](https://w2.electrodragon.com/Board-dat/ESP/ESP1000-dat/ESP1000-dat.md)

# ESP1000-dat

Module based on [SCM1030-dat](/Board-dat/SCM/SCM1030-dat/SCM1030-dat.md)

## All in one Pin Map

| ESP32 L\_Pin | ESP32\_CAM | tori      | ESP32 M\_Pin | ESP32\_CAM | tori    | ESP32 R\_Pin | ESP32\_CAM     | tori |
| ------------ | ---------- | --------- | ------------ | ---------- | ------- | ------------ | -------------- | ---- |
| GND          |            |           | GND2         |            |         | GND          |                |      |
| 3V3          |            |           | 13           | microSD    | SCL     | 23           | CAM            |      |
| EN           |            |           | SD2          | PSRAM      |         | 22           | CAM            |      |
| 36           | CAM        |           | SD3          | PSRAM      |         | TXD0         |                |      |
| 39           | CAM        |           | CMD          |            |         | RXD0         |                | PIR  |
| 34           | CAM        |           | CLK          |            |         | 21           | CAM            |      |
| 35           | CAM        |           | SD0          | PSRAM      |         | –            |                |      |
| 32           | CAM\_PWR   |           | SD1          | PSRAM      |         | 19           | CAM            |      |
| 33           |            |           | 15           | microSD    | SDA     | 18           | CAM            |      |
| 25           |            |           | 2            | microSD    | I2S\_WS | 5            | CAM            |      |
| 26           | CAM        |           |              |            |         | 17           | PSRAM          |      |
| 27           | CAM        |           |              |            |         | 16           | PSRAM          |      |
| 14           | microSD    | I2S\_SD   |              |            |         | 4            | microSD, flash |      |
| 12           | microSD    | I2S\_SCLK |              |            |         | 0            | CAM            |      |

## Board Map

![Board Map](2025-02-21-14-53-56.png)

### Programming Note

* Purple box jumper must be disconnected for enabling RXD0, otherwise used by PIR sensor
* Connect purple box by a jumper to enter into programming mode

### More Jumpers Note:

* **GND3** - disconnect pin from GND, due to an issue on [SCM1030-dat](/Board-dat/SCM/SCM1030-dat/SCM1030-dat.md) board V1701; default: does not connect
* **USB-5V** - set USB power supply, default ON, simplifies power supply
* **JP3** - set PIR sensor power supply to 3.3V, could be better at 2.5V

### Power Supply

**Version 1.1**:

* Simplified power supply; connect [serial-dat](/Tech-dat/Interface-dat/Serial-dat/Serial-dat.md) 5V / GND / TXD / RXD
* [lithium-battery-dat](/Tech-dat/power-dat/battery-dat/battery-rechargerable-dat/lithium-battery-dat/lithium-battery-dat.md) can be charged by USB or [serial-dat](/Tech-dat/Interface-dat/Serial-dat/Serial-dat.md)

**Version 1.0**:

* Top-left green box used for powering ESP32 only
* To use sensors while debugging:

  * Lithium battery + USB cable
  * USB-TTL debug power supply + USB cable

![Power Image 1](2025-02-21-14-58-48.png)
![Power Image 2](2025-02-21-14-59-03.png)

### ESP32-CAM Version Note

* Fixed by jumper in version 1.1
* Version V1701: GND3 not working, refer to [SCM1030-dat](/Board-dat/SCM/SCM1030-dat/SCM1030-dat.md). Solution: bend or cut the pin

## In Use

* [I2S-dat](/Tech-dat/Interface-dat/I2S-dat/I2S-dat.md) - [I2S-microphone-dat](/Tech-dat/Interface-dat/I2S-dat/I2S-microphone-dat/I2S-microphone-dat.md)
* [PIR-sensor-dat](/Tech-dat/Sensor-dat/Motion-sensor-dat/PIR-sensor-dat/PIR-sensor-dat.md) - [OLED-dat](/Tech-dat/interactive-dat/display-dat/OLED-dat/OLED-dat.md)
* [sensor-dat](/Tech-dat/Sensor-dat/sensor-dat.md) - [I2C-dat](/Tech-dat/Interface-dat/I2C-dat/I2C-dat.md) - [BME280-dat](/Chip-dat/bosch-dat/BME280-dat/BME280-dat.md) - [BMP280-dat](/Chip-dat/bosch-dat/BMP280-dat/BMP280-dat.md)

Refer to [BAT1002-dat](/Board-dat/BAT/BAT1002-dat/BAT1002-dat.md) for solar charge and battery function.

* [consonance-dat](/Chip-cn-dat/CONSONANCE-dat/CONSONANCE-dat.md) - [solar-power-dat](/Tech-dat/power-dat/solar-power-dat/solar-power-dat.md) - [battery-dat](/Tech-dat/power-dat/battery-dat/battery-dat.md)
* [ESP32-dat](/Chip-cn-dat/Espressif-dat/ESP32-chip-dat/ESP32-dat.md) - [SCM1030-dat](/Board-dat/SCM/SCM1030-dat/SCM1030-dat.md)

## Not in Use

* [SD-dat](/Tech-dat/memory-dat/sd-dat/sd-dat.md) - [IP5306-dat](/Chip-cn-dat/injoinic-dat/IP5306-dat/IP5306-dat.md)

## Demo Code

* BSP/ESP/ESP1000-ESP32-tori @ [https://github.com/Edragon/Arduino-ESP32](https://github.com/Edragon/Arduino-ESP32)

**Code Test**

* **T1**

  * T1.1-BMP280-PIR-OLED.ino
  * T1-all-test.ino (tests BMP280, SSD1306 OLED, PIR sensor)
* **T2**

  * T2-CameraWebServer.ino (official camera test)
* **T3**

  * T3-I2S-mem-mic.ino (tests [I2S-microphone-dat](/Tech-dat/Interface-dat/I2S-dat/I2S-microphone-dat/I2S-microphone-dat.md))

**Pin Definitions**

```cpp
#define I2S_WS 02
#define I2S_SD 14
#define I2S_SCK 12
SSD1306Wire display(0x3c, 15, 13);
BMx280I2C bmx280(0x76);

#define flash 4
#define PIR 3
```

## Demo Video

* [Default camera log (battery)](https://x.com/electro_phoenix/status/1881569671020949656)
* [I2S camera sound detect](https://x.com/electro_phoenix/status/1877590478109159437)
* [PIR sensor detector](https://x.com/electro_phoenix/status/1877256534687650008)
* [I2S sound test 2](https://t.me/electrodragon3/349)

## References

* [ESP1000](/ESP1000)
