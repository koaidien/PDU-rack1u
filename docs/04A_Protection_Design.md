# 04A_Protection_Design.md

# Protection Design Specification

USB-C PD Rack PDU

Revision A

---

# 1. Purpose

Tài liệu này mô tả toàn bộ chiến lược bảo vệ của hệ thống.

Mục tiêu:

- An toàn điện.
- Bảo vệ nguồn.
- Bảo vệ từng cổng USB-C.
- Dễ sửa chữa.
- Không để một lỗi nhỏ làm hỏng toàn bộ hệ thống.

---

# 2. Protection Philosophy

Thiết kế tuân theo các nguyên tắc:

1. AC và DC được bảo vệ độc lập.
2. Mỗi nhánh USB-C được bảo vệ riêng.
3. Hạn chế tối đa hỏng dây chuyền (Cascade Failure).
4. Không dùng linh kiện hoạt động sát giới hạn định mức.
5. Mọi linh kiện bảo vệ phải dễ thay thế.

---

# 3. Protection Layers

Hệ thống gồm 5 lớp bảo vệ.

Layer 1

AC Protection

↓

Layer 2

Main DC Protection

↓

Layer 3

Power Switching

↓

Layer 4

Branch Protection

↓

Layer 5

Monitoring

---

# 4. AC Protection

Bao gồm:

- IEC C14
- Công tắc nguồn
- Cầu chì AC

AC không đi qua PCB.

PE nối trực tiếp chassis.

---

# 5. Main DC Protection

Ngay sau nguồn Mean Well.

Thứ tự:

24V PSU

↓

Main Fuse

↓

TVS Diode

↓

Reverse Polarity MOSFET

↓

INA226

↓

Soft Latch

↓

Distribution Bus

---

# 6. Main Fuse

Mục đích

Bảo vệ toàn bộ hệ thống.

Loại

Automotive Blade Fuse hoặc Mini Blade Fuse.

Giá trị

20A

Yêu cầu

Có thể thay thế từ bên trong mà không cần tháo PCB.

---

# 7. TVS Protection

TVS đặt sát đầu vào nguồn 24V.

Chức năng

- Hấp thụ xung điện áp.
- Giảm ảnh hưởng từ việc đóng/ngắt tải.
- Bảo vệ MOSFET và module PD.

Đã chọn

**SMBJ30A** (standoff 30V, breakdown min 33.3V, clamping voltage tối đa 48.4V, 600W)

Lý do chọn 30V thay vì 28V

Mean Well RSP-500-24 có Output Voltage ADJ Range 20~26.4V và OVP trip range 27.6~32.4V. Với SMBJ28A (breakdown min 31.1V), một lỗi OVP khiến áp vọt tới 32.4V sẽ khiến TVS dẫn liên tục trước khi PSU tự ngắt. SMBJ30A (breakdown min 33.3V) nằm trên toàn bộ dải OVP fault (tối đa 32.4V), tránh được tình huống này.

---

# 8. Reverse Polarity Protection

Sử dụng

N-Channel MOSFET (IRFB4110PBF) + LM74700-Q1 ideal diode controller

Không sử dụng PMOS hoặc diode nối tiếp.

Lý do

- Sụt áp thấp (~0.05~0.06V @ 14.2A, MOSFET gần full-on ở dòng thiết kế)
- Tỏa nhiệt thấp (~0.75~0.9W, không cần heatsink — thấp hơn cả phương án trước)
- Hiệu suất cao
- Điều khiển Soft Latch qua pin EN của LM74700-Q1 (kéo EN xuống thấp → Gate về 0V, MOSFET off; nối EN lên ANODE nếu muốn always-on)

Đã thay thế (xem CHANGELOG)

IRLB8721PBF (Vds 30V) + LM5050-1 — không đủ margin điện áp so với TVS (ban đầu SMBJ28A, nay là SMBJ30A, clamping voltage tối đa 48.4V), có thể khiến MOSFET bị quá áp khi TVS dẫn.

---

# 9. Soft Latch Protection

Nguồn được bật bằng công tắc nhấn (momentary).

Soft Latch điều khiển MOSFET.

Ưu điểm

- Không mang dòng lớn qua công tắc.
- Có thể mở rộng điều khiển bằng ESP32.
- Có thể bổ sung Auto Shutdown trong tương lai.

---

# 10. Branch Protection

Mỗi module PD có:

Fuse

↓

470uF Low ESR

↓

1uF Ceramic

↓

PD Module

Các nhánh hoạt động hoàn toàn độc lập.

---

# 11. Fuse Strategy

Main Fuse

20A

↓

Branch Fuse

5A × 5

Nếu một module lỗi

↓

Chỉ mất một nhánh.

---

# 12. Capacitor Protection

Main Bus

470uF

↓

Power Control

Mỗi Branch

470uF

+

1uF

Đặt càng gần module càng tốt.

---

# 13. Ground Protection

PE

↓

Chassis

FG (PSU)

↓

Chassis

Power Ground

↓

Single Point Ground

Logic Ground

↓

Single Point Ground

Không cho dòng tải lớn chạy qua đường Logic Ground.

---

# 14. Fan Protection

Fan sử dụng nguồn từ MP1584.

Không cấp trực tiếp từ 24V.

Nếu quạt chập

↓

Không ảnh hưởng bus chính.

---

# 15. ESP32 Protection

ESP32 không tham gia điều khiển đường công suất.

Nếu ESP32 lỗi

↓

PDU vẫn hoạt động bình thường.

---

# 16. Monitoring Layer

INA226 giám sát:

- Bus Voltage
- Current
- Power

Không dùng để ngắt nguồn.

Chỉ phục vụ giám sát.

---

# 17. Thermal Protection

Revision A

2 × DS18B20 cảm biến nhiệt độ:

- T1: Gần PSU (RSP-500-24)
- T2: Gần cụm PD module

Giao tiếp: 1-Wire, chung 1 dây, header 1×3 trên Power Control Board.

Không có ngắt nguồn tự động theo nhiệt.

Revision B (Dự kiến)

ESP32

↓

DS18B20 × 2

↓

MQTT Alert

↓

Auto Shutdown (Optional)

---

# 18. Failure Analysis

Main Fuse đứt

↓

Toàn bộ hệ thống tắt.

--------------------------------

Branch Fuse đứt

↓

Chỉ mất một cổng USB-C.

--------------------------------

MOSFET lỗi

↓

Main Fuse bảo vệ.

--------------------------------

TVS hỏng

↓

Thay thế độc lập.

--------------------------------

ESP32 lỗi

↓

Mất Monitoring.

↓

Nguồn vẫn hoạt động.

--------------------------------

INA226 lỗi

↓

Mất đo dòng.

↓

Nguồn vẫn hoạt động.

---

# 19. Serviceability

Có thể thay thế riêng:

- Main Fuse
- Branch Fuse
- TVS
- MOSFET
- INA226
- ESP32

Không cần thay toàn bộ PCB.

---

# 20. Design Freeze

Revision A

Đã chốt:

✓ Main Fuse 20A

✓ Branch Fuse cho từng module

✓ TVS bảo vệ bus 24V

✓ IRFB4110PBF (NMOS, 100V) + LM74700-Q1 (ideal diode controller)

✓ Soft Latch điều khiển qua EN pin

✓ INA226 main bus (PCB shunt 2mΩ)

✓ INA226 per-port footprint dự phòng (Revision B)

✓ DS18B20 × 2 thermal monitoring

✓ Không có Auto Shutdown
