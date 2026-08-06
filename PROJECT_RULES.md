# PROJECT_RULES.md

# USB-C PD Rack PDU

Design Rules

Revision A

---

# 1. Project Goals

Thiết bị phải:

- Hoạt động liên tục 24/7
- Dễ bảo trì
- Dễ sửa chữa
- Dễ nâng cấp
- Có thể tự chế tạo
- Có thể đặt PCB tại JLCPCB
- Có thể in 3D toàn bộ khung

Không tối ưu theo tiêu chí rẻ nhất.
Ưu tiên độ ổn định và khả năng mở rộng.

---

# 2. Mechanical Rules

## 2.1 Rack

Standard

10-inch Rack

Height

1U

---

## 2.2 Front Panel

Chỉ bao gồm:

- Power Switch
- Status LED
- Fan

Không đặt USB.

---

## 2.3 Rear Panel

Bao gồm

- IEC C14
- USB-C x5
- (Optional) WiFi Antenna

---

## 2.4 Fasteners

Ưu tiên

M3

Không dùng M2 hoặc M2.5 nếu không bắt buộc.

---

## 2.5 Heat Inserts

Ưu tiên sử dụng

M3 Brass Heat Insert

Toàn bộ vị trí tháo lắp nhiều lần.

---

## 2.6 3D Printing

Khung chính

PETG

hoặc

ABS/ASA

Không khuyến nghị PLA.

---

## 2.7 Structural Design

PCB không được chịu lực.

Toàn bộ lực cắm USB truyền qua Rear Panel.

Module PD phải được cố định vào panel.

---

# 3. Electrical Rules

## 3.1 AC

220VAC

↓

IEC C14

↓

Mean Well

AC không đi qua PCB.

---

## 3.2 PE

PE

↓

Chassis

↓

Mean Well FG

Không đi qua PCB.

---

## 3.3 DC

Toàn bộ PCB chỉ làm việc ở

24VDC

---

## 3.4 Distribution

Mỗi module

↓

Fuse

↓

470uF

↓

1uF

↓

PD Module

---

## 3.5 Monitoring

INA226

Đo tại đầu vào nguồn.

Không đo từng module.

---

## 3.6 Fan

Buck Converter

↓

PWM Fan

ESP32 chỉ điều khiển PWM.

Không điều chỉnh điện áp Buck bằng phần mềm.

---

# 4. PCB Rules

## 4.1 PCB Count

Power Control Board

Power Distribution Board

Fan Board

---

## 4.2 PCB Thickness

1.6 mm

---

## 4.3 Copper

2 oz

Nếu chi phí hợp lý.

Nếu không

1 oz + tăng bề rộng đường nguồn.

---

## 4.4 Silkscreen

Tất cả connector phải ghi:

- Voltage
- Pin Name
- Direction

Ví dụ

24V IN

FAN1

I2C

UART

...

---

## 4.5 Connectors

Không dùng đầu nối độc quyền.

Ưu tiên:

- JST-XH
- KF301
- Pin Header 2.54 mm

---

## 4.6 Test Points

Mỗi board phải có:

24V

GND

3V3

I2C

UART

---

# 5. Component Rules

Ưu tiên linh kiện phổ biến tại Việt Nam.

Nếu phải đặt quốc tế

↓

LCSC

↓

Mouser

↓

DigiKey

---

Module thương mại

Không thiết kế lại.

Ví dụ

MP1584

USB PD

ESP32

...

---

# 6. Software Rules

ESP32

Optional

Không ảnh hưởng hoạt động thiết bị.

Nếu ESP hỏng

↓

PDU vẫn hoạt động bình thường.

---

# 7. Maintainability

Có thể thay:

- PSU
- Quạt
- PD Module
- ESP32
- Fan Board

không cần tháo toàn bộ thiết bị.

---

# 8. Wiring Rules

AC

↓

Một phía

DC

↓

Một phía

Không đi chung.

---

Dây AC

↓

Bó riêng.

---

Dây DC

↓

Bó riêng.

---

# 9. Documentation Rules

Mọi quyết định thiết kế

↓

Cập nhật CHANGELOG.

---

Không sửa BOM trực tiếp.

Mọi thay đổi BOM

↓

Tăng Revision.

---

# 10. Naming Convention

PCB

PCB-PWR

PCB-DIST

PCB-FAN

---

Connector

Jxx

---

Fuse

Fxx

---

Capacitor

Cxx

---

MOSFET

Qxx

---

IC

Uxx

---

LED

Dxx

---

# 11. Future Compatibility

Thiết kế phải cho phép:

- PD 100W
- INA228
- Ethernet ESP32
- OLED
- Temperature Sensors

không phải thay đổi kiến trúc.

---

# 12. Out of Scope

Không hỗ trợ:

- PoE
- Battery Backup
- UPS
- Lithium Charging
- AC Output
- USB Hub

Thiết bị chỉ là USB-C Power Distribution Unit.

# 13. Design Philosophy

Khi có nhiều phương án khả thi, ưu tiên theo thứ tự sau:

1. Safety
   - An toàn điện luôn là ưu tiên cao nhất.
   - AC và DC phải được cách ly rõ ràng.
   - Không đánh đổi an toàn để giảm chi phí.

2. Reliability
   - Thiết bị phải hoạt động ổn định 24/7.
   - Không sử dụng linh kiện chạy sát giới hạn định mức.

3. Serviceability
   - Mọi module phải có thể tháo và thay thế độc lập.
   - Không yêu cầu tháo toàn bộ thiết bị để sửa một thành phần.

4. Simplicity
   - Ưu tiên giải pháp đơn giản, dễ hiểu và dễ sửa.
   - Tránh thêm tính năng nếu không mang lại lợi ích rõ ràng.

5. Availability
   - Ưu tiên linh kiện phổ biến tại Việt Nam.
   - Nếu phải nhập khẩu, ưu tiên LCSC để thuận tiện khi đặt PCB tại JLCPCB.

6. Expandability
   - Mọi thiết kế cần chừa khả năng mở rộng trong tương lai (ESP32, giám sát, PD 100W...) mà không phải thay đổi kiến trúc tổng thể.
