# USB-C PD Rack PDU

> 10-inch 1U USB-C Power Distribution Unit

Revision: A (Planning)

---

## Giới thiệu

Đây là dự án thiết kế một bộ USB-C Power Distribution Unit (PDU) dành cho rack 10 inch.

Thiết bị sử dụng nguồn AC 220V chuyển đổi sang 24VDC, sau đó phân phối tới 5 module USB-C PD 65W độc lập.

Mục tiêu là tạo ra một thiết bị:

- dễ chế tạo
- dễ sửa chữa
- dễ nâng cấp
- phù hợp Homelab
- hoạt động 24/7

---

## Đặc điểm

- 5 × USB-C PD 65W
- Nguồn Mean Well 24V
- Theo dõi dòng điện bằng INA226
- ESP32-C3 (tùy chọn)
- Quạt PWM
- Rack 10 inch 1U
- Thiết kế dạng module
- PCB tách thành nhiều board

---

## Kiến trúc

220VAC

↓

IEC C14 + Fuse + Switch

↓

Mean Well 24V

↓

Power Control Board

↓

Power Distribution Board

↓

5 × USB-C PD Module

↓

USB Devices

---

## PCB

- Power Control Board
- Power Distribution Board
- Fan Board

---

## Tình trạng

Current Phase

✔ Planning

---

## Roadmap

- Mechanical Design
- Schematic
- PCB Layout
- 3D Print
- Assembly
- Firmware
- Testing

