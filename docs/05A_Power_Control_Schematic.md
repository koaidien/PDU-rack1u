# Power Control Schematic

---

# Functional Blocks

24V Input

↓

Main Fuse

↓

TVS

↓

Reverse MOSFET

↓

INA226

↓

Soft Latch

↓

Distribution Output

↓

Fan Supply

↓

ESP32 Header

---

# Contains

Main Fuse

TVS

MOSFET

INA226

Soft Latch

MP1584

Fan Header

ESP32 Header

Programming Header

Status LED

Power LED

---

# Excludes

USB PD Module

Branch Fuse

470uF Branch

---

# Signal Flow

Power Switch

↓

Soft Latch

↓

MOSFET

↓

24V Bus

---

# Interfaces

Input

J1

24V

Output

J2

24V BUS

Fan

J3

ESP

J4

I²C

J5

UART

---

# Test Points

TP1

24V

TP2

3V3

TP3

PGND

TP4

LGND

TP5

I²C

TP6

UART

---

# Acceptance

✓ ERC Clean

✓ Current Path Verified

✓ Fuse Correct

✓ TVS Correct

✓ MOSFET Direction Verified
