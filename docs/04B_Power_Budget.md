# 04B_Power_Budget.md

# Power Budget and Electrical Load Analysis

USB-C PD Rack PDU

Revision A

---

# 1. Purpose

Tài liệu này xác định:

- Công suất thiết kế.
- Dòng điện tối đa.
- Công suất dự phòng.
- Kích thước bus nguồn.
- Điều kiện hoạt động liên tục.

---

# 2. Design Target

Hệ thống gồm:

5 × USB-C PD Module

Maximum

65W / module

Tổng công suất danh nghĩa:

325W

---

# 3. Input Power

Nguồn

Mean Well LRS-350-24

Output

24VDC

Rated Power

350W

Rated Current

14.6A

---

# 4. Expected Load

| Thiết bị | Công suất |
|-----------|----------:|
| PD1 | 65W |
| PD2 | 65W |
| PD3 | 65W |
| PD4 | 65W |
| PD5 | 65W |

Maximum

325W

---

# 5. Practical Load

Thiết kế hướng tới tải thực tế:

250~300W

Lý do

Trong hầu hết trường hợp sử dụng, không phải tất cả các cổng đều hoạt động ở công suất cực đại cùng lúc.

---

# 6. Control Board Consumption

| Thiết bị | Công suất |
|-----------|----------:|
| INA226 | <0.1W |
| ESP32-C3 | <1W |
| MP1584 | <1W |
| Logic | <1W |

Tổng

≈3W

---

# 7. Fan Consumption

Hai quạt PWM

0.25A mỗi quạt

12V

≈6W

Tổng

≈12W

Giá trị thực tế phụ thuộc loại quạt sử dụng.

---

# 8. Total Estimated Power

USB Modules

≈325W

Control Board

≈3W

Fans

≈12W

Tổng

≈340W

---

# 9. Current Calculation

340W

÷24V

≈14.2A

Thiết kế bus

20A Continuous

---

# 10. Safety Margin

Bus

20A

Expected

≈14A

Margin

≈30%

---

# 11. Branch Current

65W

÷24V

≈2.7A

Thiết kế

5A mỗi nhánh

---

# 12. Wiring

Main Bus

AWG16

Branch

AWG18 hoặc AWG20 (tùy chiều dài)

Signal

AWG24

---

# 13. PCB Current

Power Control

20A

Distribution

20A

Mục tiêu

Không để bất kỳ đoạn đồng nào hoạt động vượt quá 70% khả năng chịu dòng thiết kế.

---

# 14. Copper Recommendation

Ưu tiên

2 oz Copper

Nếu dùng 1 oz

↓

Tăng chiều rộng đường nguồn hoặc sử dụng copper pour.

---

# 15. Heat Generation

Nguồn nhiệt chính:

1. Mean Well PSU
2. 5 × PD Modules
3. MOSFET (không đáng kể nếu chọn đúng)
4. MP1584 (thấp)

Các linh kiện logic không được coi là nguồn nhiệt đáng kể.

---

# 16. Thermal Budget

Thiết kế yêu cầu:

Luồng gió Front → Rear

Heatsink trên từng module PD

Khe hở giữa các heatsink

Không khí đi xuyên qua các lá tản nhiệt

---

# 17. Future Expansion

Nếu chuyển sang:

100W × 5

↓

500W

Revision A

KHÔNG hỗ trợ.

Cần:

- PSU lớn hơn
- Bus lớn hơn
- PCB mới

---

# 18. Power Budget Summary

| Hạng mục | Giá trị |
|----------|---------:|
| PSU | 350W |
| USB PD | 325W |
| Logic | ~3W |
| Fan | ~12W |
| Tổng | ~340W |
| Bus Design | 20A |

---

# 19. Design Notes

- Thiết kế ưu tiên hoạt động ổn định 24/7.
- Không giả định tất cả cổng luôn tải cực đại.
- Dành khoảng dự phòng cho tổn hao và điều kiện môi trường.

---

# 20. Design Freeze

Revision A

Đã chốt:

✓ 24VDC Architecture

✓ 5 × PD65W

✓ Mean Well LRS-350-24

✓ 20A Main Bus

✓ AWG16 Main Wiring

✓ 2 oz Copper (ưu tiên)

✓ Thermal-first Design
