# System Block Diagrams

USB-C PD Rack PDU

Revision A

---

# 1. Overview

Toàn bộ hệ thống được chia thành các khối độc lập.

Mỗi khối chỉ đảm nhiệm một chức năng.

```
                AC Input

                   │

                   ▼

          Mean Well Power Supply

                   │

                   ▼

          Power Control Board

                   │

     ┌─────────────┴─────────────┐

     ▼                           ▼

Distribution Board          Fan Board

     │

     ▼

PD1 PD2 PD3 PD4 PD5
```

---

# 2. Electrical Block Diagram

```
220VAC

│

▼

IEC C14
Switch
Fuse

│

▼

Mean Well PSU

24VDC

│

▼

Power Control Board

│

├──────────────► Fan Board

│

└──────────────► Distribution Board

                     │

     ┌────┬────┬────┬────┬────┐

     ▼    ▼    ▼    ▼    ▼

    PD1  PD2  PD3  PD4  PD5
```

---

# 3. Power Flow

```
220VAC

↓

Fuse

↓

Switch

↓

Mean Well

↓

24VDC

↓

Main Fuse

↓

MOSFET

↓

Distribution Bus

↓

Branch Fuse

↓

PD Module

↓

USB Device
```

---

# 4. Signal Flow

```
INA226

│

▼

I2C

│

▼

ESP32

│

├────► MQTT

├────► Web UI

└────► Home Assistant
```

---

# 5. Fan Control Flow

```
24V

↓

MP1584

↓

Fan

▲

│ PWM

ESP32
```

ESP32 chỉ điều khiển PWM.

Không điều chỉnh điện áp đầu ra của MP1584.

---

# 6. Monitoring Flow

```
24V Input

↓

INA226

↓

Voltage

Current

Power

↓

ESP32

↓

MQTT

↓

Dashboard
```

---

# 7. Board Connections

```
            Power Control Board

                │

        24V BUS │

                ▼

      Distribution Board

        │ │ │ │ │

        ▼ ▼ ▼ ▼ ▼

      PD PD PD PD PD

                │

                └────► Fan Board
```

---

# 8. Wiring Diagram

```
AC Side

IEC

│

├── L

├── N

└── PE

        │

        ▼

     Mean Well

DC Side

V+

V-

↓

Power Control
```

AC và DC luôn đi hai bó dây riêng.

---

# 9. Ground Diagram

```
PE

↓

Chassis

↓

Mean Well FG

---------------------

24V Return

↓

Distribution Board

↓

PD Modules
```

Không nối PE qua PCB.

---

# 10. Airflow

```
Front

┌──────────────┐

Fan

>>>>>

Power Supply

>>>>>

Power Control

>>>>>

Distribution

>>>>>

PD Modules

└──────────────┘

Rear
```

Luồng gió luôn theo một chiều.

---

# 11. Mechanical Zones

```
+--------------------------------------+

| PSU | PCB Area | USB Modules |

+--------------------------------------+

Front

Power

LED

Fan

Rear

IEC

USB

USB

USB

USB

USB
```

---

# 12. Safety Zones

```
+-----------+

 AC ZONE

+-----------+

        ||

Isolation

        ||

+-----------+

24V ZONE

+-----------+

        ||

+-----------+

Logic Zone

+-----------+
```

Không để AC chạy vào Logic Zone.

---

# 13. Maintenance Flow

```
Hỏng Module

↓

Mở nắp

↓

Rút Module

↓

Thay Module

↓

Lắp lại

↓

Hoạt động
```

Không cần tháo PSU.

---

# 14. Failure Diagram

```
PD1 Fault

↓

Fuse1

↓

Only PD1 Off

------------------

ESP32 Fault

↓

Monitoring Off

↓

Power Still On

------------------

Fan Fault

↓

Temperature Warning

↓

Power Still On
```

---

# 15. Future Expansion

```
ESP32

│

├── Ethernet

├── OLED

├── Temperature

├── MQTT

└── Home Assistant
```

Không thay đổi kiến trúc nguồn.

---

# 16. Wiring Philosophy

```
AC

LEFT

RIGHT

DC

----------------

POWER

TOP

SIGNAL

BOTTOM
```

Không bó AC và tín hiệu chung.

---

# 17. Service Philosophy

Có thể tháo riêng:

✓ PSU

✓ Power Control Board

✓ Distribution Board

✓ Fan Board

✓ USB Module

✓ Fan

✓ ESP32

Không ảnh hưởng các khối khác.

---

# 18. Architecture Summary

```
220VAC

↓

IEC

↓

Mean Well

↓

Power Control

↓

Distribution

↓

5 × PD

↓

USB Devices
```

Đây là kiến trúc chính thức của Revision A.
