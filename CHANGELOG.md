# Changelog

## Revision A (Updated 2026-08-07)

### Component Decisions

- PSU: **Mean Well RSP-500-24** (504W/21A, fan tích hợp, 199×97×38mm)
- PD Module: Samirob/diymore DC 8-30V → USB-C 65W, **direct solder**
- Fan: **4040 4-pin PWM**, ball bearing, phía trước, mua sau
- MOSFET: **IRLB8721PBF (NMOS) + LM5050-1** (gate driver, LCSC C473393)
- Thermal: **DS18B20 × 2** (T1: PSU, T2: cụm PD), 1-Wire
- INA226 main bus: PCB shunt **R002 2mΩ 2512 3W 1%**
- INA226 per-port (Rev B): module Feiyang, đổi shunt sang **R010 10mΩ 2512 3W 1%**

### Mechanical

- Rack 10 inch
- Height 1U
- PSU bên phải
- PCB bên trái
- USB-C phía sau
- Quạt phía trước

### Electrical

- 5 USB PD 65W
- INA226
- ESP32 footprint
- MP1584 Fan Board
- Soft Latch
- High-side MOSFET

### AC

- IEC AC-14-F16C
- Screw Mount
- Fuse
- Switch

### Future

- MQTT
- Home Assistant
- OLED
- OLED Statistics
- Temperature Monitoring

