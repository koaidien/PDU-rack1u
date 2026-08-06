# 03A_Mechanical_Envelope.md

USB-C PD Rack PDU

Mechanical Envelope Specification

Revision A

---

# 1. Purpose

Tài liệu này định nghĩa:

- Kích thước tối đa của từng board.
- Khoảng hở cơ khí.
- Keep-out Zone.
- Component Height.
- Cable Space.
- Airflow Space.
- Mounting Hole.
- Screw Location.

Mọi thiết kế PCB và CAD phải tuân theo tài liệu này.

---

# 2. Rack Envelope

Standard

10-inch Rack

Height

1U

Maximum External Dimensions

Width

≤ 250 mm

Depth

≤ 180 mm

Height

44.45 mm

---

# 3. Internal Envelope

Sau khi trừ:

- panel trước
- panel sau
- nắp

không gian sử dụng khoảng:

Width

≈235 mm

Depth

≈165 mm

Maximum Internal Height

≈39 mm

---

# 4. Height Zones

Đây là thông số quan trọng nhất.

## Zone A

PCB thông thường

Maximum Component Height

15 mm

Ví dụ

- IC
- Header
- TVS
- MOSFET

---

## Zone B

Power Components

Maximum

20 mm

Ví dụ

- Electrolytic Capacitor
- Fuse Holder

---

## Zone C

USB PD Modules

Maximum

28 mm

---

## Zone D

Mean Well PSU

Theo datasheet

Không giới hạn bởi PCB.

---

# 5. Board Envelope

## Power Control Board

Maximum

80 × 60 mm

Recommended

75 × 55 mm

Height

≤20 mm

---

## Distribution Board

Maximum

170 × 50 mm

Recommended

165 × 45 mm

Height

≤25 mm

---

## Fan Board

Maximum

60 × 40 mm

Recommended

55 × 35 mm

Height

≤18 mm

---

# 6. Keep-out Zones

## Around PSU

Minimum Clearance

10 mm

Không đặt:

- PCB
- Dây tín hiệu
- ESP32

---

## Around Fan

Minimum

5 mm

Không đặt dây chắn gió.

---

## Around USB Modules

Minimum

3 mm

Để thay module.

---

## Around IEC

Minimum

10 mm

Không đi dây DC.

---

# 7. PCB Clearance

PCB

↓

Wall

Minimum

2 mm

---

PCB

↓

PSU

Minimum

5 mm

---

PCB

↓

PCB

Minimum

3 mm

---

# 8. Airflow Envelope

Luồng gió

Front

↓

Fan

↓

PSU

↓

Power Control

↓

Distribution

↓

USB Modules

↓

Rear

Không có vật cản kín hoàn toàn.

---

# 9. Cable Envelope

## AC Cable

Một phía.

Không giao với DC.

Minimum Bend Radius

25 mm

---

## DC Cable

AWG16

Bend Radius

20 mm

---

## Signal Cable

I²C

UART

PWM

Đi sát thành chassis.

---

# 10. Mounting Hole Standards

Power PCB

4 holes

M3

---

Distribution

4 holes

M3

---

Fan Board

2 holes

M3

---

# 11. Standoff Height

PCB

↓

Standoff

6 mm

Recommended

Nylon hoặc Brass.

---

# 12. Heat Insert

Standard

M3

Outer Diameter

≈5 mm

Depth

5 mm

Material

Brass

---

# 13. Screw Length

PCB

M3×8

---

Panel

M3×10

---

Fan

M4×20

---

PSU

Theo datasheet Mean Well

---

# 14. USB Module Position

Module

↓

Rear Panel

↓

USB-C Flush

Dung sai

±0.5 mm

PCB không dùng để căn chỉnh đầu USB-C.

---

# 15. IEC Position

IEC C14

↓

Rear Panel

↓

Screw Mount

Không dùng Snap-in.

---

# 16. Power Button Position

Front Panel

Center Height

≈22 mm

LED hướng ra ngoài.

---

# 17. Fan Position

Front Panel

Centered

Để tạo luồng gió đối xứng.

---

# 18. PCB Keep-out

Không đặt linh kiện tại:

- Góc bắt vít
- Mép PCB 3 mm
- Sau đầu nối KF301
- Sau đầu nối JST

---

# 19. Copper Keep-out

Khoảng cách tối thiểu:

Copper

↓

Board Edge

0.5 mm

---

Copper

↓

Mounting Hole

1.5 mm

---

# 20. Service Envelope

Phải có đủ khoảng hở để:

✓ Thay nguồn

✓ Thay quạt

✓ Thay từng module PD

✓ Rút ESP32

Không cần tháo toàn bộ hệ thống.

---

# 21. Manufacturing Constraints

PCB

JLCPCB Standard

1.6 mm

2 oz Copper (ưu tiên)

HASL Lead-Free hoặc ENIG

---

3D Printing

Layer Height

0.20 mm

Nozzle

0.40 mm

Material

PETG

Wall

≥2.4 mm

Top/Bottom

≥1.2 mm

Infill

25–35%

---

# 22. Thermal Expansion

Chừa khe hở tối thiểu:

0.5 mm

giữa các chi tiết in 3D.

---

# 23. Reserved Volume

Chừa khoảng:

80 × 30 × 20 mm

cho các mở rộng trong tương lai:

- OLED
- Ethernet ESP32
- Relay
- INA228
- Temperature Hub

---

# 24. Mechanical Freeze

Các thông số sau được coi là cố định trong Revision A:

✓ Rack 10 inch 1U

✓ PSU bên phải

✓ PCB bên trái

✓ USB-C phía sau

✓ Fan phía trước

✓ PCB không chịu lực

✓ Rear Panel chịu lực USB

✓ M3 Heat Insert

✓ M3 Screw

✓ Không dùng Snap-fit

✓ Không để AC đi chung bó với DC

Mọi thay đổi các thông số trên phải tăng Revision.
