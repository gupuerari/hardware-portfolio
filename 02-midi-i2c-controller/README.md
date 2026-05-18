# MIDI to I²C Controller

> A compact MIDI input device that exposes received MIDI messages on an I²C bus for integration with embedded host systems.

**Role:** Hardware design — schematic and PCB layout
**Status:** Delivered · ⭐⭐⭐⭐⭐ on Upwork
**Client:** European (English-speaking)
**Tools:** KiCad

---

## Context

The client needed a small, dedicated controller that could receive standard MIDI input and expose the resulting messages on an I²C bus, so they could be consumed by a host embedded system. The deliverable was a complete, manufacturable PCB design.

## Solution

A small-form-factor board centered on a MIDI-to-I²C bridge IC, with standard MIDI 1.0 input circuitry (5-pin DIN connector, opto-isolated input per the MIDI electrical specification) and 3.3 V I²C output to the host.

## Design Highlights

- **MIDI 1.0 compliance** — opto-isolated input meeting the original electrical specification, ensuring compatibility with the widest range of MIDI sources and avoiding ground-loop issues common in audio environments.
- **Compact layout** — minimum footprint to allow embedding the board inside larger musical or instrumented products.
- **Manufacturability** — generic, widely sourceable components and a DFM-friendly layout suitable for low-volume contract assembly.

## Outcome

Delivered on time and within scope. Client review: **5 stars** on Upwork.

---

## Tech Stack

`MIDI 1.0` · `I²C` · `KiCad`

## Confidentiality

Client-identifying details and the full design files are private. The description above is public-safe and intended for portfolio demonstration only.
