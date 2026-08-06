# Project Requirements

## 1. Mục tiêu

Thiết kế một USB-C PDU cho rack 10 inch.

Thiết bị phải:

- ổn định
- hoạt động 24/7
- dễ bảo trì
- dễ nâng cấp

---

## 2. Electrical Requirements

Input

- 220VAC

Main PSU

- Mean Well LRS-350-24
or
- Mean Well LRS-450-24

Output

5 × USB-C PD Module

Maximum

5 × 65W

---

## 3. Mechanical Requirements

Rack

10 inch

Height

1U

Front

- Power Button
- Status LED
- Fan

Rear

- IEC C14
- 5 USB-C

---

## 4. Monitoring

Current

INA226

Controller

ESP32-C3

Features

- MQTT
- Web UI
- Home Assistant
- OTA

---

## 5. Cooling

One adjustable buck converter

↓

PWM Fan

↓

Air duct

↓

PSU

↓

USB PD Modules

---

## 6. Maintainability

PCB phải tháo rời.

Module PD phải thay được.

Quạt thay được.

Nguồn thay được.

Không cần tháo toàn bộ thiết bị.

---

## 7. Design Rules

### Electrical

- AC không đi qua PCB
- Chỉ có 24VDC trên PCB
- Mỗi module có fuse riêng
- Mỗi module có tụ 470uF

### Mechanical

- Screw Mount
- Heat Insert M3
- Không dùng Snap-fit
- PCB không chịu lực cắm USB

### PCB

Power Control Board

Power Distribution Board

Fan Board

---

## 8. Future Expansion

ESP32

↓

Temperature

↓

OLED

↓

Power Statistics

↓

Ethernet / WiFi

↓

MQTT

↓

Home Assistant
