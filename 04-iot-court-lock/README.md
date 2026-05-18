# IoT Lock for Sports Courts

> A small integration board for access control to tennis and padel courts, deployed alongside the LoRaWAN scoring system in the same facility ecosystem.

**Role:** Hardware design — schematic and PCB layout
**Status:** Delivered
**Tools:** KiCad

---

## Context

The client needed a simple but reliable access-control board to combine an off-the-shelf electromagnetic lock, an ESP32 controller module, and an I²C status display into a single integrated assembly. The deliverable was a clean PCB tying these pre-built components together with appropriate power management and protection.

## Solution

A minimal-component integration board:

- **ESP32 module** (off-the-shelf) for Wi-Fi connectivity and control logic
- **Driver and protection circuitry** for the electromagnetic lock
- **I²C interface** for the status display
- **Input regulation and protection** appropriate for outdoor sports facility environments

## Design Highlights

- **Component reuse over redesign** — all functional blocks use proven off-the-shelf modules, reducing risk and time-to-deployment while keeping the assembly clean and field-serviceable.
- **Power protection** — input protection circuitry suited for outdoor environments and intermittent operation.
- **Ecosystem fit** — designed to be deployed alongside the LoRaWAN scoring system at the same facility, with consistent installation and maintenance practices.

## Outcome

Delivered and deployed. Operates in conjunction with the LoRaWAN scoring system at the same sports facility.

---

## Tech Stack

`ESP32` · `I²C` · `KiCad`

## Confidentiality

Client details and design files are private. The description above is public-safe and intended for portfolio demonstration only.
