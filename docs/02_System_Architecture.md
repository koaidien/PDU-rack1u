# System Architecture

USB-C PD Rack PDU

Revision A

---

# 1. System Overview

USB-C PD Rack PDU là một thiết bị phân phối nguồn USB-C PD
dành cho rack 10 inch.

Thiết bị gồm các module độc lập:

- AC Input
- DC Power Supply
- Power Control Board
- Power Distribution Board
- Fan Board
- ESP32 Monitoring (Optional)

Tất cả được thiết kế theo dạng module để dễ bảo trì và mở rộng.

---

# 2. High Level Architecture

                    AC 220V
                       │
                       ▼
          IEC C14 + Switch + Fuse
                       │
                       ▼
               Mean Well PSU
                24VDC Output
                       │
                       ▼
             Power Control Board
                       │
            ┌──────────┴──────────┐
            │                     │
            ▼                     ▼
 Power Distribution Board     Fan Board
            │
            │
 ┌────┬────┬────┬────┬────┐
 ▼    ▼    ▼    ▼    ▼
PD1  PD2  PD3  PD4  PD5
 │    │    │    │    │
 ▼    ▼    ▼    ▼    ▼
USB  USB  USB  USB  USB

---

# 3. Functional Blocks

## AC Input

Bao gồm:

- IEC C14
- Power Switch
- Fuse

Nhiệm vụ:

- Cấp nguồn AC
- Ngắt nguồn
- Bảo vệ quá dòng

Không đi qua PCB.

---

## Mean Well PSU

Input

220VAC

↓

Output

24VDC

↓

Power Control Board

---

## Power Control Board

Là bộ điều khiển nguồn chính.

Bao gồm:

- Main Fuse
- TVS
- INA226
- Soft Latch
- High-side MOSFET
- ESP32 Header

Chức năng

- Bảo vệ nguồn
- Giám sát dòng
- Đóng/ngắt nguồn
- Cấp nguồn cho Distribution Board

---

## Power Distribution Board

Nhận:

24VDC

↓

Phân phối

↓

5 module USB-C PD

Mỗi module:

Fuse

↓

470uF

↓

1uF

↓

USB PD Module

Các nhánh hoạt động độc lập.

---

## Fan Board

Nhận:

24V

↓

MP1584

↓

5~12V

↓

PWM Fan

Không liên quan đến Power Control.

---

## ESP32

(Optional)

Đọc

INA226

↓

MQTT

↓

Home Assistant

↓

Web UI

Nếu ESP32 hỏng

↓

Thiết bị vẫn hoạt động.

---

# 4. Power Flow

220VAC

↓

IEC

↓

Mean Well

↓

24VDC

↓

Power Control

↓

Distribution

↓

USB PD

↓

USB Device

---

# 5. Signal Flow

INA226

↓

I2C

↓

ESP32

↓

WiFi

↓

MQTT

↓

Home Assistant

---

# 6. Mechanical Layout

Front

Power Button

Status LED

Fan

========================

Inside

Power Supply

Power Control

Distribution

Fan Board

========================

Rear

IEC C14

USB-C ×5

---

# 7. Power Domains

Domain 1

AC 220V

------------------------

Domain 2

24VDC

------------------------

Domain 3

Buck Output

5~12V

------------------------

Domain 4

3V3

ESP32

INA226

---

# 8. Safety Zones

Zone A

AC

- IEC
- Fuse
- Switch
- Mean Well Input

Zone B

24V

Power PCB

Zone C

Low Voltage Logic

ESP32

INA226

I2C

Không để AC đi vào Zone B hoặc Zone C.

---

# 9. Data Interfaces

Power Control

↓

I2C

↓

ESP32

ESP32

↓

UART

Programming

ESP32

↓

WiFi

MQTT

---

# 10. Cooling Path

Front Fan

↓

Power Supply

↓

Power Control

↓

Distribution

↓

USB PD

↓

Rear Exhaust

Luồng gió chỉ theo một chiều.

---

# 11. Failure Strategy

Nếu:

ESP32 lỗi

↓

PDU vẫn hoạt động.

------------------------

INA226 lỗi

↓

PDU vẫn hoạt động.

------------------------

Một module PD lỗi

↓

Các module còn lại vẫn hoạt động.

------------------------

Fan lỗi

↓

PDU vẫn hoạt động

↓

Cảnh báo sau này bằng ESP32.

---

# 12. Future Expansion

Thiết kế phải hỗ trợ:

- INA228
- OLED
- Ethernet ESP32
- Temperature Sensors
- USB PD 100W Module

Không thay đổi kiến trúc tổng thể.

---

# 13. Architecture Principles

- PCB không chịu lực cơ khí.
- AC và DC tách biệt hoàn toàn.
- Một chức năng chỉ thuộc một board.
- Mỗi board có thể tháo và thay thế độc lập.
- Không có điểm lỗi đơn làm mất toàn bộ hệ thống (ngoại trừ nguồn chính).

---

# 14. Board Responsibilities

Power Control Board

- Power Switching
- Protection
- Monitoring

Power Distribution Board

- Power Distribution
- Branch Protection

Fan Board

- Cooling

ESP32

- Telemetry
- Automation

Mean Well

- AC/DC Conversion

Rear Panel

- Mechanical Support

Front Panel

- User Interface

---

# 15. Design Freeze (Revision A)

Các quyết định đã chốt:

✓ Rack 10 inch 1U

✓ Mean Well LRS Series

✓ IEC AC-14-F16C (Screw Mount)

✓ 5 × USB-C PD 65W

✓ INA226

✓ ESP32-C3 Optional

✓ MP1584 Mini Module

✓ Module PD gắn đứng

✓ PCB không chịu lực USB

✓ Front chỉ có Power + Fan

✓ Rear gồm IEC + USB-C

Các thay đổi lớn sau thời điểm này phải tăng Revision.
