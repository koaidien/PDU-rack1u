# Changelog

## Revision A (Updated 2026-08-07)

### Component Decisions

- PSU: **Mean Well RSP-500-24** (504W/21A, fan tích hợp, 199×97×38mm)
- PD Module: Samirob/diymore DC 8-30V → USB-C 65W, **direct solder**
- Fan: **4040 4-pin PWM**, ball bearing, phía trước, mua sau
- MOSFET: **IRFB4110PBF (NMOS, 100V, TO-220AB) + LM74700-Q1** (ideal diode controller, SOT-23-6) — thay cho IRLB8721PBF/LM5050-1 vì không đủ margin Vds so với TVS SMBJ28A
- TVS: **SMBJ30A** (standoff 30V, clamp 48.4V max) — thay cho SMBJ28A vì SMBJ28A (breakdown min 31.1V) không đủ margin so với dải OVP fault của RSP-500-24 (27.6~32.4V)
- Thermal: **DS18B20 × 2** (T1: PSU, T2: cụm PD), 1-Wire
- INA226 main bus: PCB shunt **R002 2mΩ 2512 3W 1%**
- INA226 per-port (Rev B): module Feiyang, đổi shunt sang **R010 10mΩ 2512 3W 1%**

### Mechanical

- Rack 10 inch
- Height 1U
- PSU bên phải
- PCB bên trái
- USB-C phía sau
- Quạt phía trước

### Electrical

- 5 USB PD 65W
- INA226
- ESP32 footprint
- MP1584 Fan Board
- Soft Latch
- High-side MOSFET
- Fan header: **3× PWM 4-pin (J6, J7, J9)** — J9 dự phòng cho quạt bổ sung, không bắt buộc lắp ở Revision A

### AC

- IEC AC-14-F16C
- Screw Mount
- Fuse
- Switch

### Future

- MQTT
- Home Assistant
- OLED
- OLED Statistics
- Temperature Monitoring

---

### Documentation Fixes (2026-08-07)

- **01_Project_Requirements.md**: đồng bộ Main PSU thành Mean Well RSP-500-24 (trước đó ghi LRS-350-24 / LRS-450-24, không khớp Component Decisions).
- **04B_Power_Budget.md**: đồng bộ Input Power (504W / 21A) và Design Freeze theo RSP-500-24; bổ sung mục margin riêng cho PSU (~48%) bên cạnh margin bus (~30%).
- **04A_Protection_Design.md** / **04C_Component_Selection.md**: sửa lỗi đảo giá trị shunt INA226 trong mục Freeze — main bus **2mΩ** (không phải 10mΩ), khớp với Component Selection §5 và BOM.
- **02B_Connector_and_Interface_Spec.md**: thêm **J9 — PWM Fan Header 3** (dự phòng), renumber các mục 13→21 theo sau; cập nhật Interface Freeze.
- **05C_BOM_Preliminary.md**: cập nhật số lượng fan header từ ×2 lên ×3.
- **04A_Protection_Design.md** / **04C_Component_Selection.md** / **05C_BOM_Preliminary.md**: đổi MOSFET reverse-protection từ IRLB8721PBF (30V) sang IRFB4110PBF (100V) và gate driver từ LM5050-1 sang LM74700-Q1. Lý do: TVS SMBJ28A clamp tối đa ~45.4V vượt quá Vds 30V của IRLB8721PBF, gần như không có margin khi TVS dẫn. IRFB4110PBF cho margin ~120%, đồng thời Rds(on) thấp hơn (3.7mΩ so với 8mΩ) giúp giảm tổn hao.
- **04_Electrical_Design.md**: cập nhật quy tắc chọn MOSFET (§15) để margin điện áp tính theo clamping voltage của TVS phía trước, không chỉ theo 24V bus danh nghĩa — tránh lặp lại vấn đề margin này ở Revision B.
- **04A_Protection_Design.md** / **04C_Component_Selection.md** / **04_Electrical_Design.md** / **05C_BOM_Preliminary.md**: chốt TVS từ SMBJ28A sang **SMBJ30A**. Lý do: tra datasheet Mean Well RSP-500-24 cho thấy Output ADJ Range 20~26.4V và OVP trip range 27.6~32.4V — SMBJ28A (breakdown min 31.1V) có thể dẫn liên tục nếu PSU lỗi OVP (áp vọt tới 32.4V), trong khi SMBJ30A (breakdown min 33.3V) nằm an toàn trên toàn dải OVP fault. Đã cập nhật lại margin MOSFET/gate driver theo clamp voltage mới của SMBJ30A (48.4V thay vì 45.4V) — IRFB4110PBF vẫn còn margin ~107%, LM74700-Q1 vẫn còn margin ~34%, cả hai vẫn đủ dùng, không cần đổi linh kiện.

