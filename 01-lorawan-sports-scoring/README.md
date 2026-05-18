# LoRaWAN Sports Scoring System

> A three-tier hardware system for live court-side score tracking on tennis and padel courts.

**Role:** Hardware design — schematic and PCB layout for all three boards
**Status:** In production · Three devices delivered
**Tools:** KiCad · EasyEDA · custom component libraries
**Client:** Confidential (private engagement)

---

## Context

A sports facility needed a way to display live match scores on court-side TVs across multiple tennis and padel courts. Existing solutions were either wired (impractical for outdoor courts), short-range (Bluetooth, unreliable through bodies and structures), or too power-hungry (requiring frequent recharging).

The system needed to be **battery-powered, long-range, and low-maintenance** — a court controller running for months between charges, while remaining responsive to score changes in real time.

## System Architecture

The system is split into three hardware tiers, each with distinct constraints:

```
   ┌──────────────┐    LoRa (sub-GHz)   ┌──────────────┐   Wi-Fi / Ethernet   ┌──────────────┐
   │  Controller  │ ──────────────────▶ │   Gateway    │ ───────────────────▶ │   Display    │
   │   (battery)  │      via SX1262     │  (V1 or V2)  │                      │  application │
   └──────────────┘                     └──────────────┘                      └──────────────┘
```

- **Controller** — court-side device with score-input buttons. Battery-powered, optimized for multi-month operation.
- **Gateway** — receives radio packets from controllers and forwards them to the display application.
- **Display application** — runs on a TV-connected device showing real-time scores. *(Software layer, not part of this engagement.)*

---

## Device 1 — Controller

A handheld, battery-powered device with exposed GPIOs for an external button panel. The user presses physical buttons to update scores; the controller transmits each change over LoRa.

| Parameter | Choice |
|---|---|
| MCU | **STM32L031K6** (Cortex-M0+, ultra-low-power) |
| Radio | **Semtech SX1262** (LoRa, sub-GHz) |
| I/O | GPIOs exposed to external button panel |
| Power | Single Li-ion cell |
| Achieved battery life | **3+ months between charges** |

**Why STM32L031K6?**
The L0 family is among the lowest-power Cortex-M0+ options at this price point. Combined with aggressive sleep states and event-driven wake (button press or scheduled keep-alive), the MCU is asleep for the vast majority of operating time. System current in standby falls well below 10 µA.

**Why SX1262 over older SX127x?**
Lower TX/RX consumption, lower sleep current, and an integrated DC-DC for the receiver — all of which directly extend battery life. Also improved LoRa link budget for environments with obstructions and bodies between transmitter and receiver, which matters on a busy court.

---

## Device 2 — Gateway V1

The first-generation gateway receives LoRa packets from controllers and forwards them to the display application over Wi-Fi.

| Parameter | Choice |
|---|---|
| MCU | **ESP32-S3** |
| LoRa front-end | SX1262 |
| Connectivity | Wi-Fi |
| Wired interface | USB |
| Power | USB-powered (no battery constraint) |

**Why ESP32-S3?**
At the time of V1 design, S3 offered the best combination of dual-core performance, native USB-OTG, and Wi-Fi for the gateway role — handling LoRa reception, Wi-Fi backhaul, and the USB connection to the display device in parallel.

---

## Device 3 — Gateway V2

A second-generation gateway built to address two needs that emerged in field operation: **lower BOM cost** and an **Ethernet option** for installations where Wi-Fi proved unreliable.

| Parameter | Choice |
|---|---|
| MCU | **ESP32-C3** |
| LoRa front-end | SX1262 |
| Wireless | Wi-Fi |
| Wired interface | **Ethernet via Wiznet W5500** (SPI) |
| Power | USB-powered |

**Why move from ESP32-S3 to ESP32-C3?**
Lower cost, smaller footprint, and the workload of the gateway (LoRa reception plus uplink) does not require dual-core performance or USB-OTG. The C3's single RISC-V core handles the role comfortably.

**Why add Ethernet?**
In larger facilities, Wi-Fi proved unreliable due to network congestion and distance from access points. Adding the **Wiznet W5500** SPI-Ethernet controller provides a wired alternative without changing the system architecture or display application. The same firmware abstraction handles either link.

---

## Hardware Design Highlights

- **RF layout for sub-GHz LoRa** — antenna routing with controlled impedance, proper ground plane structure, RF keep-out zones, and matching network design.
- **Power architecture for multi-month battery** — careful selection of LDOs and DC-DC stages on the controller to minimize quiescent current while supporting LoRa TX bursts without sag.
- **Mixed-signal isolation** — separating digital MCU activity from the sensitive RF front-end on a compact shared board.
- **Custom component library** — KiCad and EasyEDA symbols and footprints created from scratch for non-standard parts, validated against manufacturer specifications.
- **Generational iteration** — V2 gateway re-architected based on V1 field data, with measurable improvements in cost and deployment flexibility.

## Outcome

All three devices entered production. Controllers consistently meet the 3+ month battery-life target in real-world usage. The V2 gateway is in active deployment alongside V1 units, offering both Wi-Fi-only and Wi-Fi + Ethernet configurations based on site conditions.

---

## Tech Stack

`STM32L031K6` · `Semtech SX1262` · `LoRa / LoRaWAN` · `ESP32-S3` · `ESP32-C3` · `Wiznet W5500` · `KiCad` · `EasyEDA`

## Confidentiality

This case study is published with the client's identifying details, full schematics, PCB layouts, and firmware kept private. The architectural and engineering content above is public-safe and intended for portfolio demonstration only.
