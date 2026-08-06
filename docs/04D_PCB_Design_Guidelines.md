# 04D_PCB_Design_Guidelines.md

# PCB Design Guidelines

USB-C PD Rack PDU

Revision A

---

# 1. Purpose

Quy định thiết kế PCB.

Áp dụng cho:

- PCB-CTRL
- PCB-DIST

---

# 2. PCB Stackup

FR4

1.6mm

2 Layer

Ưu tiên

2oz Copper

---

# 3. Board Separation

PCB-CTRL

- Điều khiển
- Giám sát
- Quạt

PCB-DIST

- Phân phối nguồn
- Fuse
- Tụ
- Pad module PD

Không trộn chức năng.

---

# 4. Power Routing

Không dùng trace hẹp.

Ưu tiên

Copper Pour

Polygon

Wide Trace

---

# 5. Copper Width

Main Bus

Thiết kế cho

20A Continuous

Không dựa hoàn toàn vào IPC tối thiểu.

Ưu tiên dư tải.

---

# 6. Ground

Power Ground

Logic Ground

Tách riêng.

Single Point Ground.

---

# 7. Placement Rules

Nguồn vào

↓

Fuse

↓

TVS

↓

MOSFET

↓

INA226

↓

Distribution

Theo đúng chiều dòng điện.

---

# 8. Capacitor Placement

470uF

≤20mm

so với điểm cấp nguồn module.

1uF

Đặt sát chân module.

---

# 9. Thermal Rules

Không đặt tụ điện sát:

- MOSFET
- TVS
- Buck Converter

Đảm bảo có luồng gió.

---

# 10. Fan Section

MP1584

Đặt gần đầu quạt.

Biến trở quay ra mép PCB.

---

# 11. Keep-out

Không đặt linh kiện:

- Dưới module PD
- Sát lỗ bắt vít
- Sát mép PCB (<3mm)

---

# 12. Test Points

PCB-CTRL

- TP_24V
- TP_GND
- TP_3V3
- TP_I2C
- TP_UART

PCB-DIST

- TP_IN
- TP_OUT
- TP_GND

---

# 13. Silkscreen

Mọi đầu nối đều ghi:

Tên

Điện áp

Chiều tín hiệu

Ví dụ

24V IN

FAN1

I2C

UART

---

# 14. Mounting

M3 Hole

NPTH

Không đi đồng dưới spacer.

---

# 15. Design for Assembly

Có thể hàn tay.

Không dùng package quá nhỏ.

Ưu tiên

0805

1206

SOT-223

TO-252

---

# 16. PCB Revision

Định dạng

PCB-CTRL-REV-A

PCB-DIST-REV-A

---

# 17. Manufacturing

JLCPCB Standard

Không dùng công nghệ đặc biệt.

---

# 18. PCB Freeze

Revision A

Đã chốt:

✓ 2 PCB

✓ 2 Layer

✓ 2oz Copper

✓ Copper Pour

✓ Direct Solder PD Module

✓ Thermal-first Layout
