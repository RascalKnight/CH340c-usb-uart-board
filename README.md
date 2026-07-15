# USB-C to UART Converter Board

A 2-layer PCB that bridges USB-C to a TTL UART interface, built from 
scratch in KiCad using the CH340C USB-to-serial chip. Designed as a 
self-directed learning project to understand USB-C connector requirements, 
UART fundamentals, and full-cycle PCB design (schematic, layout, routing, 
and DRC resolution).

## Overview

This board allows a computer to communicate with a microcontroller or 
other UART-based device over USB-C, exposing TX, RX, GND, and VCC on a 
simple header. It replaces the need for a legacy USB-A to serial adapter 
with a compact, modern USB-C native solution.

## Key Design Features

- **CH340C** USB-to-UART bridge IC (crystal-less variant, integrated 
  clock)
- **USB-C receptacle (16P)** with correctly implemented CC1/CC2 pull-down 
  resistors (5.1kΩ) for proper USB-C power negotiation as a UFP (device)
- Standard **VBUS decoupling** (10µF + 0.1µF) and **V3 pin decoupling** 
  per CH340C's 5V power configuration
- Direct D+/D- routing from the USB-C connector to the CH340C's UD+/UD- 
  pins, verified pin-by-pin against the datasheet to avoid a reversed 
  connection
- 4-pin 2.54mm header output (VCC, GND, TXD, RXD) for standard jumper 
  wire compatibility

## Design Challenges Solved

- Diagnosed a **thermal relief spoke count DRC error** on the MCU's 
  fine-pitch GND pads, resolved by switching to a solid zone connection 
  for those specific pads
- Identified and resolved a **hole clearance violation** between the 
  USB-C connector's mechanical mounting holes and adjacent GND pads, 
  distinguishing it from a standard copper clearance issue
- Corrected a **decoupling capacitor placement issue** during layout 
  review, moving caps to sit directly against their associated IC pins
- Fixed an incorrect **RESET pull-up voltage rail** (was tied to 5V on a 
  3.3V-powered MCU) during an earlier related board, applying that lesson 
  here for correct voltage domain separation

## Files

- `.kicad_sch` / `.kicad_pcb` — full KiCad source project
- Schematic PDF export
- 3D board render

## Tools

Designed entirely in KiCad 10.

## Status

Schematic and layout complete, DRC clean. Not yet fabricated/assembled.