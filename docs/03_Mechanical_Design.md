# 03_Mechanical_Design.md

USB-C PD Rack PDU

Mechanical Design Specification

Revision A

---

# 1. Design Goals

Thiết kế cơ khí phải đáp ứng các mục tiêu sau:

- Dễ in 3D.
- Dễ lắp ráp.
- Dễ bảo trì.
- Không truyền lực lên PCB.
- Dễ thay thế từng module.
- Tương thích rack 10 inch.
- Luồng gió một chiều.

---

# 2. Rack Standard

Type

10-inch Rack

Height

1U

Nominal Height

44.45 mm

Material

3D Printed Chassis

Recommended Material

PETG

Optional

ABS

ASA

Không khuyến nghị PLA cho sử dụng lâu dài.

---

# 3. Overall Layout

Top View

```

┌──────────────────────────────────────────────────────┐

│                                                      │

│ PSU │ PCB AREA │

│ │ │

│ │ Distribution │

│ │ │

│ │ Power Ctrl │

│ │ │

│ │ Fan Board │

│                                                      │

└──────────────────────────────────────────────────────┘

```

PSU đặt bên phải.

PCB đặt bên trái.

Không giao nhau.

---

# 4. Front Panel

Front chỉ bao gồm:

- Power Button
- Status LED
- Fan Intake

Không đặt:

- USB
- Connector
- Programming Port

---

# 5. Rear Panel

Rear gồm:

- IEC C14 AC-14-F16C
- USB-C x5
- Optional WiFi Antenna

Không đặt quạt.

---

# 6. Airflow

```

Front

↓

Fan

↓

Power Supply

↓

Power Control

↓

Distribution

↓

USB Modules

↓

Rear

```

Không để luồng gió vòng.

---

# 7. Mechanical Zones

## Zone A

AC Input

Bao gồm:

IEC

Switch

Fuse

AC Wiring

---

## Zone B

Power Supply

Mean Well

---

## Zone C

Power Electronics

Power Control

Distribution

---

## Zone D

Logic

ESP32

INA226

---

## Zone E

USB Modules

---

# 8. Structural Philosophy

PCB không chịu lực.

Lực cắm USB

↓

Rear Panel

↓

Main Chassis

Không truyền vào PCB.

---

# 9. Module Mounting

USB PD Module

↓

Rear Panel

↓

Spacer

↓

PCB

PCB chỉ định vị điện.

Không chịu tải cơ học.

---

# 10. PCB Mounting

Ưu tiên:

M3 Brass Insert

↓

M3 Screw

↓

Spacer

Không dùng:

Snap-fit

Glue

---

# 11. PSU Mounting

Mean Well

↓

M4 Screw

↓

Printed Bracket

↓

Main Chassis

Có khe thoát nhiệt.

---

# 12. Fan Mounting

120 mm

hoặc

80 mm

tùy phiên bản.

Dùng:

M4 Screw

Rubber Damper (Optional)

---

# 13. Fan Board

Fan Board đặt ngay sau quạt.

Mục tiêu:

Giảm chiều dài dây.

---

# 14. Power Control Board

Đặt sát nguồn.

Khoảng cách:

<100 mm

---

# 15. Distribution Board

Đặt sát Rear Panel.

Module PD hàn trực tiếp.

USB-C thò ra panel.

---

# 16. Wiring

AC

↓

Một bó riêng.

DC

↓

Một bó riêng.

Signal

↓

Một bó riêng.

Không buộc chung.

---

# 17. Service Access

Có thể thay:

PSU

↓

Không tháo PCB

----------------

Có thể thay:

Fan

↓

Không tháo PSU

----------------

Có thể thay:

USB Module

↓

Không tháo toàn bộ hệ thống

---

# 18. Fasteners

Chuẩn chung:

M3

Nguồn:

M4

Heat Insert

M3 Brass

---

# 19. Cable Management

Ưu tiên:

Zip Tie Mount

Cable Clip

Printed Channel

Không để dây lơ lửng.

---

# 20. Tolerance

PCB Clearance

>=2 mm

PSU Clearance

>=5 mm

USB Module Clearance

>=2 mm

Fan Clearance

>=3 mm

---

# 21. Future Expansion

Chừa vị trí cho:

ESP32

OLED

Temperature Sensor

Không cần sửa chassis.

---

# 22. Manufacturing

PCB

JLCPCB

3D Print

Bambu

Creality

Prusa

Hardware

M3 Standard

---

# 23. Assembly Sequence

1. Gắn heat insert.
2. Lắp nguồn.
3. Lắp Power Control.
4. Lắp Distribution.
5. Lắp Fan Board.
6. Lắp quạt.
7. Đi dây AC.
8. Đi dây DC.
9. Kiểm tra.
10. Đóng nắp.

---

# 24. Mechanical Freeze

Revision A

Đã khóa:

✓ PSU bên phải.

✓ PCB bên trái.

✓ USB phía sau.

✓ Fan phía trước.

✓ PCB không chịu lực.

✓ Rear Panel chịu lực USB.

✓ Heat Insert M3.

✓ Screw Mount.

