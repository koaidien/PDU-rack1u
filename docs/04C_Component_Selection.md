# 04C_Component_Selection.md

# Component Selection Specification

USB-C PD Rack PDU

Revision A

---

# 1. Purpose

Tài liệu này quy định tiêu chí lựa chọn linh kiện.

Mục tiêu:

- Hoạt động 24/7.
- Dễ mua tại Việt Nam.
- Có thể thay thế.
- Không phụ thuộc một nhà cung cấp.

---

# 2. Selection Philosophy

Ưu tiên theo thứ tự:

1. Độ tin cậy
2. Hiệu suất
3. Khả năng thay thế
4. Giá thành
5. Kích thước

Không chọn linh kiện chỉ vì rẻ.

---

# 3. Power Supply

Khuyến nghị

**Mean Well RSP-500-24**

Thông số

- Output: 24VDC / 21A / 504W
- Kích thước: 199 × 97 × 38mm
- Cooling: Fan tích hợp (active)
- PFC tích hợp
- Remote ON/OFF
- Remote Sense

Yêu cầu

- Output 24VDC
- Hiệu suất >88%
- Hoạt động liên tục
- Có bảo vệ OVP/OCP/OTP

⚠️ Lưu ý cơ khí

RSP-500-24 có fan tích hợp thổi hướng ngang.
Cần kiểm tra conflict airflow với fan 4040 phía trước khi hoàn thiện mechanical layout.

---

# 4. USB PD Module

Loại

Commercial PD Trigger Module

Sản phẩm đã chọn

Samirob / diymore PD65W DC Input

Input

DC 8~30V (tương thích 24V)

Output

USB-C PD3.1 / QC3.0 / SCP

Maximum

65W

Yêu cầu

- DC Input 8~32V
- Hiệu suất >90%
- Có lỗ bắt heatsink

Lắp đặt

Direct solder vào Distribution Board.
Không dùng connector trung gian.
Pad phải đủ lớn cho AWG18.

Không sửa đổi thiết kế module.

---

# 5. Current Monitor

## Main Bus

INA226

Shunt resistor

**R002 — 2mΩ, 2512, 3W, 1%**

Giao tiếp

I²C

Điện áp

3.3V

Mục đích: đo tổng dòng vào hệ thống.

Thông số đã xác nhận

- Sụt áp @ 20A: 40mV (trong dải 81.92mV của INA226)
- Tổn hao @ 20A: 0.8W → 3W rating, margin 73%
- Dòng đo tối đa: 40.96A
- Độ phân giải: ~1.25mA/LSB

## Per-Port Monitoring (Revision B)

Module Feiyang INA226 breakout

Shunt: đổi R100 mặc định sang **R010 — 10mΩ, 2512, 3W, 1%**

Lý do: 65W / 24V ≈ 2.7A per port

- Sụt áp @ 2.7A: 27mV → đọc tốt
- Tổn hao @ 2.7A: 0.073W → 3W rating, margin 97%
- Dòng đo tối đa: 8.19A
- Độ phân giải: ~0.25mA/LSB
- Việc đổi shunt không ảnh hưởng linh kiện khác trên module
- Chỉ cần cập nhật calibration register trong firmware

Revision A: chừa footprint shunt + I2C header, chưa lắp module.
Revision B: lắp 5 module, dùng TCA9548A I2C mux.

---

# 6. ESP32

ESP32-C3

Optional

Module dạng DevKit

Không hàn cố định.

---

# 7. Buck Converter

MP1584EN Mini Module

Input

24V

Output

5~12V

Điều chỉnh bằng biến trở.

Biến trở hướng ra mặt trước.

---

# 8. MOSFET + Gate Driver

Phương án: NMOS High-side + Charge Pump Controller

## Switch

IRLB8721PBF

- Loại: N-Channel MOSFET
- Vds: 30V
- Id: 62A
- Rds(on): 8mΩ
- Package: TO-220
- Tổn hao @ 14A: ~1.6W (không cần heatsink)
- Nguồn: LCSC / phổ biến

## Gate Driver

LM5050-1 (TI)

- Chức năng: High-side NMOS controller + charge pump
- Vin: 5~75V (phù hợp 24V)
- Package: SC70-5
- LCSC: C473393 (~$1.17)
- Điều khiển Soft Latch qua pin EN

Alternative

LM74700 (TI) — LCSC, tương tự LM5050, gate drive mạnh hơn

⚠️ Không dùng SY6280 — chỉ hỗ trợ đến 5.5V.

---

# 9. TVS

SMBJ Series

Điện áp kẹp phù hợp bus 24V

Package

SMB

---

# 10. Fuse

Main

Mini Blade Fuse

20A

Branch

Mini Blade hoặc Pico Fuse

5A

---

# 11. Capacitor

Main Bus

470uF

35V

105°C

Low ESR

---

Branch

470uF

35V

105°C

Low ESR

---

Ceramic

1uF

50V

X7R

---

# 12. Fan

Kích thước: **40 × 40 × 40mm (4040)**

Loại: 4-pin PWM

Điện áp: 12V

Vị trí: Mặt trước (intake)

Bearing: Dual Ball (bắt buộc cho 24/7)

Không dùng Sleeve Bearing.

Mua sau — cần kiểm tra conflict airflow với RSP-500-24 trước khi chốt.

---

# 13. Connectors

Power

Hàn trực tiếp

Signal

JST-XH

UART

2.54 Pin Header

Fan

PC PWM Header

---

# 14. PCB

FR4

1.6mm

2oz Copper (ưu tiên)

ENIG hoặc HASL LF

---

# 15. Mechanical Hardware

Heat Insert

M3 Brass

Spacer

M3 Nylon

Screw

M3 Stainless

---

# 16. Preferred Vendors

Việt Nam

- Hshop
- Linh Kiện 3M
- Điện tử Nhất Anh

Quốc tế

- LCSC
- Mouser
- DigiKey

---

# 17. Component Lifetime

Electrolytic Capacitor

105°C

≥5000 giờ

Fan

≥50.000 giờ

PSU

Theo datasheet Mean Well

---

# 18. Thermal Monitoring

Sensor: **DS18B20**

Số lượng: **2 chiếc**

Giao tiếp: 1-Wire (chung 1 dây, phân biệt bằng 64-bit ROM ID)

Vị trí:

- T1: Gần PSU (RSP-500-24)
- T2: Gần cụm PD module

Revision A: chừa header 1-Wire 1×3 trên Power Control Board.

---

# 19. Component Freeze

Revision A

Đã chốt:

✓ Mean Well RSP-500-24

✓ Samirob/diymore PD65W DC input

✓ INA226 (main bus, PCB shunt 2mΩ)

✓ IRLB8721 + LM5050-1

✓ DS18B20 × 2

✓ ESP32-C3

✓ MP1584

✓ Mini Blade Fuse

✓ 470uF Low ESR

✓ JST-XH

✓ M3 Hardware

✓ Fan 4040 4-pin PWM (mua sau)
