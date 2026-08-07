# Electrical Design Specification

USB-C PD Rack PDU

Revision A

---

# 1. Purpose

Tài liệu này định nghĩa:

- Kiến trúc nguồn.
- Bảo vệ.
- Phân phối nguồn.
- Giám sát.
- Điều khiển.
- Điều kiện hoạt động.

Tài liệu này là cơ sở để thiết kế schematic.

---

# 2. Electrical Overview

Power Path

220VAC

↓

IEC C14

↓

Fuse

↓

Power Switch

↓

Mean Well LRS

↓

24VDC

↓

Power Control Board

↓

Power Distribution Board

↓

5 × USB-C PD Module

---

# 3. Power Input

Input Voltage

220VAC

Frequency

50Hz

Maximum Power

400W

Connector

IEC C14 Screw Mount

Ground

PE nối trực tiếp chassis.

---

# 4. DC Bus

Output Voltage

24VDC

Nominal

24.0V

Maximum Current

20A

Wire

AWG16

Topology

Star Distribution

Không mắc nối tiếp các module.

---

# 5. Main Protection

Main Fuse

20A

TVS

24V

Reverse Protection

MOSFET

Soft Latch

Có

---

# 6. Branch Protection

Mỗi module PD gồm:

Fuse

↓

470uF Low ESR

↓

1uF Ceramic

↓

PD Module

Không dùng chung cầu chì.

---

# 7. Voltage Domains

Domain A

220VAC

-------------------

Domain B

24VDC

-------------------

Domain C

Buck Output

5~12V

-------------------

Domain D

3V3 Logic

---

# 8. Grounding

PE

↓

Chassis

-------------------

24V Return

↓

Power Ground

-------------------

Logic Ground

↓

Power Ground

Một điểm nối chung (single-point ground).

---

# 9. Monitoring

INA226

Đo:

Voltage

Current

Power

Bus Location

Ngay sau Main Fuse.

---

# 10. ESP32

Optional

Không ảnh hưởng hoạt động.

Nếu ESP32 lỗi

↓

PDU vẫn cấp nguồn.

---

# 11. Fan Supply

Nguồn

24V

↓

MP1584EN

↓

5~12V

↓

PWM Fan

Điện áp chỉnh bằng biến trở.

PWM điều khiển bởi ESP32 (tương lai).

---

# 12. USB PD Modules

Quantity

5

Input

24V

Output

USB-C PD

Maximum

65W/module

Module thương mại

Không sửa thiết kế.

---

# 13. Capacitors

Main Bus

470uF

↓

Power Control

Branch

470uF

↓

Mỗi module

Ceramic

1uF

↓

Sát chân module

---

# 14. Fuse Rating

Main Fuse

20A

Branch Fuse

5A (tạm thời)

Giá trị sẽ xác nhận theo đặc tính thực tế của module PD.

---

# 15. MOSFET

High-side

Low RDS(on)

Vds ≥ margin tối thiểu 25% so với **clamping voltage tối đa của TVS đặt phía trước** (không chỉ so với 24V bus danh nghĩa).

Revision A

TVS SMBJ30A: clamping voltage tối đa 48.4V

↓

Yêu cầu tối thiểu: Vds ≥ 48.4V × 1.25 ≈ 60.5V

↓

Đã chọn: **IRFB4110PBF (Vds 100V, Rds(on) 3.7mΩ typ)** — margin ~107%

Lịch sử: Revision A ban đầu dùng IRLB8721PBF (30V) + TVS SMBJ28A, không đủ margin. Đã đổi MOSFET sang IRFB4110PBF, sau đó đổi TVS sang SMBJ30A để có margin tốt hơn so với dải OVP của PSU (xem CHANGELOG).

---

# 16. TVS

24V System

**SMBJ30A** (standoff 30V, clamp max 48.4V)

Đặt sát đầu vào nguồn.

---

# 17. Buck Converter

Module

MP1584EN

Input

24V

Output

5~12V

Adjustable

Có

Biến trở hướng ra mặt trước.

---

# 18. Connectors

Power

Hàn trực tiếp

Signal

JST-XH

Fan

PC 4-pin PWM

---

# 19. Test Points

Power Control

24V

GND

3V3

I²C

UART

Distribution

24V

GND

Fan

VIN

VOUT

---

# 20. Design Margins

Điện áp

≥25%

Dòng

≥30%

Nhiệt độ

≥20°C

Không vận hành linh kiện ở giới hạn định mức.

Lưu ý: với linh kiện đặt ngay sau TVS (ví dụ MOSFET bảo vệ), margin điện áp phải tính theo clamping voltage của TVS, không chỉ theo điện áp bus danh nghĩa (xem §15).

---

# 21. Failure Behaviour

Main Fuse đứt

↓

Toàn bộ hệ thống tắt.

----------------

Một Branch Fuse đứt

↓

Chỉ mất một cổng PD.

----------------

ESP32 lỗi

↓

Mất giám sát.

↓

Nguồn vẫn hoạt động.

----------------

Fan lỗi

↓

Không ngắt nguồn.

↓

Cảnh báo khi có ESP32.

---

# 22. Reserved Features

INA228

OLED

NTC

DS18B20

Ethernet ESP32

Relay

---

# 23. Design Freeze

Đã chốt:

✓ 24V Architecture

✓ Mean Well LRS

✓ INA226

✓ MP1584EN

✓ ESP32-C3 Optional

✓ 5 × PD65W

✓ Soft Latch

✓ Main Fuse

✓ Branch Fuse

✓ TVS (SMBJ30A)

✓ High-side MOSFET (IRFB4110PBF + LM74700-Q1, Vds margin tính theo TVS clamp)

Mọi thay đổi phải cập nhật CHANGELOG.
