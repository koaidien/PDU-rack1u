# Schematic Design

USB-C PD Rack PDU

Revision A

---

# 1. Purpose

Tài liệu này mô tả cấu trúc schematic của dự án.

Không chứa sơ đồ nguyên lý chi tiết mà định nghĩa:

- Cách chia schematic
- Thứ tự triển khai
- Quan hệ giữa các sheet
- Quy tắc review

---

# 2. Schematic Hierarchy

Project

├── Sheet 1
│   AC Input
│
├── Sheet 2
│   Power Control
│
├── Sheet 3
│   Distribution
│
├── Sheet 4
│   Fan Supply
│
└── Sheet 5
    ESP32 / Monitoring

---

# 3. Design Order

Không vẽ toàn bộ cùng lúc.

Thứ tự:

1.
Power Control

↓

2.
Distribution

↓

3.
Fan Supply

↓

4.
ESP32 Header

↓

5.
Monitoring

---

# 4. Rules

Không copy schematic.

Sử dụng Hierarchical Sheet.

---

# 5. Libraries

Ưu tiên

KiCad Official

Custom Library

↓

Project Local

---

# 6. Review Flow

Specification

↓

Schematic

↓

ERC

↓

Peer Review

↓

PCB

---

# 7. Deliverables

Sau Phase 5 sẽ có:

- *.kicad_sch
- PDF
- Netlist
- BOM
- ERC Report

---

# 8. Freeze

Sau khi schematic được review:

↓

Không đổi interface giữa các board.
