# M.2 Modular Keyboard Pedal Platform

> A hardware platform that adopts the M.2 form factor to make musical keyboard pedal functionality modular and swappable.

**Role:** Hardware design — schematic and PCB layout
**Status:** Active engagement · in progress
**Client:** European (English-speaking)
**Tools:** KiCad

---

## Context

The client is building a modular system for musical keyboard pedals, where individual functions (connectivity, processing, audio paths) are implemented as **swappable M.2 form-factor modules** plugged into a common carrier board. This allows musicians and integrators to mix and match modules without redesigning the host hardware.

## Scope

Three boards are part of this engagement:

1. **Main carrier board** — provides M.2 sockets, power distribution, and common I/O for the system.
2. **Wi-Fi module** — based on **ESP32-P4**, providing wireless connectivity in M.2 form factor.
3. **FPGA module** — provides reconfigurable digital processing for audio or control paths.

## Design Challenges

- **High-density routing on M.2** — the form factor is compact and constrained; routing mixed signal types (power, high-speed digital, control) within those limits requires disciplined floorplanning.
- **Coherent pin allocation across the edge connector** — defining a pin map that accommodates the diverse needs of different module types (wireless, FPGA, future modules) while staying compatible across the family.
- **Per-module BOM optimization** — keeping costs aligned with the musical-instrument market, which is price-sensitive at the per-pedal level.

## Status

In active development. The carrier board and Wi-Fi module are at the schematic and layout phases at the time of writing. This README will be expanded as the engagement progresses and additional details become public-safe.

---

## Tech Stack

`M.2 form factor` · `ESP32-P4` · `FPGA` · `KiCad`

## Confidentiality

Client identity, full specifications, and design files remain private throughout this engagement. The description above represents the public-safe portion of the work.
