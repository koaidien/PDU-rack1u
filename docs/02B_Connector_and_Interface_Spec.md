# Connector and Interface Specification

USB-C PD Rack PDU

Revision A

---

# 1. Purpose

Tài liệu này định nghĩa toàn bộ giao tiếp giữa các board.

Mục tiêu:

- Chuẩn hóa connector.
- Dễ bảo trì.
- Không phụ thuộc vị trí lắp đặt.
- Có thể thay thế từng board độc lập.

---

# 2. Connector Naming Convention

| Prefix | Ý nghĩa |
|---------|----------|
| J | Connector |
| JP | Jumper |
| TP | Test Point |
| F | Fuse |
| SW | Switch |
| LED | Indicator |
| FAN | Fan Header |

Ví dụ

J1

J2

TP1

TP2

---

# 3. Connector Standards

## Power

Ưu tiên

KF301

hoặc

Euroblock

Pitch

5.08 mm

Lý do

- chịu dòng lớn
- dễ đấu dây
- dễ thay thế

---

## Signal

Ưu tiên

JST-XH

Pitch

2.54 mm

---

## Debug

Pin Header

2.54 mm

---

## Fan

Chuẩn PC Fan

4 Pin

PWM Compatible

---

# 4. Board Interfaces

```
Mean Well

↓

J1

↓

Power Control

↓

J2

↓

Distribution

↓

J3

↓

Fan Board

```

---

# 5. J1

## Mean Well → Power Control

Type

KF301-2P

Voltage

24VDC

Maximum Current

20A

Pinout

| Pin | Signal |
|------|---------|
|1|24V|
|2|GND|

Recommended Wire

AWG16

---

# 6. J2

## Power Control → Distribution

Type

KF301-2P

Voltage

24V

Maximum Current

20A

Pinout

|Pin|Signal|
|---|------|
|1|24V|
|2|GND|

---

# 7. J3

## Distribution → Fan Board

Type

JST-XH 2P

Voltage

24V

Maximum Current

2A

Pinout

|Pin|Signal|
|---|------|
|1|24V|
|2|GND|

---

# 8. J4

## INA226

I²C Interface

Type

JST-XH 4P

Voltage

3.3V

Pinout

|Pin|Signal|
|---|------|
|1|3V3|
|2|GND|
|3|SCL|
|4|SDA|

---

# 9. J5

## ESP32 UART

Type

Pin Header 1×6

Pinout

|Pin|Signal|
|---|------|
|1|3V3|
|2|GND|
|3|TX|
|4|RX|
|5|BOOT|
|6|RESET|

---

# 10. J6

## PWM Fan Header 1

Type

PC Fan 4 Pin

Pinout

|Pin|Signal|
|---|------|
|1|GND|
|2|+V|
|3|TACH|
|4|PWM|

---

# 11. J7

## PWM Fan Header 2

Giống J6.

---

# 12. J8

## AUX Output

Type

JST-XH 2P

Voltage

Buck Output

Configurable

5~12V

Maximum Current

3A

---

# 13. Test Points

Power Control

TP1

24V

TP2

GND

TP3

3V3

TP4

I²C

TP5

UART

---

Distribution

TP10

24V

TP11

GND

---

Fan Board

TP20

VIN

TP21

VOUT

TP22

GND

---

# 14. Wire Colors

|Signal|Color|
|------|------|
|24V|Red|
|GND|Black|
|3V3|Orange|
|I²C SDA|Blue|
|I²C SCL|Green|
|PWM|Yellow|
|TACH|White|
|PE|Green/Yellow|
|AC Live|Brown|
|AC Neutral|Blue|

---

# 15. Wire Gauge

|Current|Recommended|
|---------|-----------|
|<1A|AWG24|
|1~3A|AWG22|
|3~5A|AWG20|
|5~10A|AWG18|
|10~20A|AWG16|

---

# 16. Maximum Cable Length

|Interface|Max Length|
|----------|-----------|
|24V Main|200 mm|
|I²C|150 mm|
|UART|150 mm|
|PWM Fan|300 mm|

Nếu vượt quá cần xem xét lại bố trí cơ khí.

---

# 17. Connector Orientation

Nguyên tắc:

- Đầu nối nguồn quay về phía nguồn.
- Đầu nối tín hiệu quay về phía ESP32.
- Không để dây nguồn và dây tín hiệu giao nhau.

---

# 18. Labeling Rules

Mọi connector đều phải có silkscreen:

Ví dụ

```

J1
24V IN

```

```

J2
24V OUT

```

```

J6
FAN1

```

Không chỉ ghi J1, J2.

---

# 19. Reserved Interfaces

Dành cho Revision B trở đi.

## J30

OLED

I²C

---

## J31

Temperature Sensor

1-Wire

---

## J32

GPIO Expansion

ESP32

---

## J33

Relay Output

Reserved

---

# 20. Interface Freeze

Các interface sau được coi là đã khóa (Revision A):

✓ J1 24V IN

✓ J2 24V OUT

✓ J3 Fan Power

✓ J4 INA226

✓ J5 UART

✓ J6 Fan1

✓ J7 Fan2

✓ J8 AUX OUT

Mọi thay đổi phải cập nhật CHANGELOG và tăng Revision.
