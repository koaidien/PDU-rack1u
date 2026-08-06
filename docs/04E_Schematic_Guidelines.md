# 04E_Schematic_Guidelines.md

# Schematic Design Guidelines

USB-C PD Rack PDU

Revision A

---

# 1. Purpose

Quy định cách xây dựng sơ đồ nguyên lý.

Mục tiêu:

- Dễ đọc.
- Dễ review.
- Dễ bảo trì.
- Dễ chuyển sang PCB.

---

# 2. Sheet Organization

Sheet 1

Power Input

Sheet 2

Power Control

Sheet 3

Power Distribution

Sheet 4

Fan Supply

Sheet 5

Monitoring

Sheet 6

ESP32 Header

---

# 3. Net Naming

Không dùng:

VCC

5V

12V

Đúng:

24V_MAIN

24V_BRANCH1

24V_BRANCH2

3V3_LOGIC

PGND

LGND

PE

---

# 4. Reference Designators

Fuse

F1...

Capacitor

C1...

Resistor

R1...

MOSFET

Q1...

IC

U1...

Connector

J1...

Test Point

TP1...

---

# 5. Connector Names

Theo tài liệu

02B_Connector_and_Interface_Spec.md

Không đổi tên.

---

# 6. Branch Replication

5 nhánh PD phải giống nhau.

Không thay đổi giá trị linh kiện giữa các nhánh nếu không có lý do kỹ thuật.

---

# 7. Annotation

Mọi linh kiện phải có:

- Value
- Footprint
- Manufacturer Part Number (nếu đã xác định)

---

# 8. Notes

Thêm ghi chú tại các vị trí quan trọng:

Ví dụ

"Place close to MOSFET"

"Low ESR Required"

"Keep trace short"

---

# 9. ERC

Yêu cầu

0 Error

0 Warning

trước khi chuyển PCB.

---

# 10. Libraries

Ưu tiên

KiCad Official Library

Nếu tự tạo footprint

↓

Lưu trong thư mục project.

Không sửa thư viện gốc.

---

# 11. Version Control

Mỗi thay đổi schematic

↓

Cập nhật CHANGELOG

↓

Tăng Revision nếu thay đổi ảnh hưởng PCB.

---

# 12. Design Review Checklist

Trước khi vẽ PCB phải kiểm tra:

□ Tất cả fuse đúng giá trị

□ TVS đúng chiều

□ MOSFET đúng hướng

□ INA226 đúng địa chỉ

□ ESP32 Header đúng pin

□ Fan Header đúng chuẩn

□ Branch giống nhau

□ Test Point đầy đủ

□ Silkscreen thống nhất

---

# 13. Design Freeze

Revision A

Đã chốt:

✓ 24V Architecture

✓ 2 PCB

✓ 5 Branch

✓ Direct Solder PD Module

✓ ESP32 Optional

✓ INA226 Monitoring

✓ MP1584 Fan Supply

✓ KiCad Native Workflow
