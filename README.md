# Comparative Study of Telescopic OTA vs. Two-Stage Miller-Compensated OTA

Design, hand-calculation, and SPICE-level simulation of two CMOS Operational Transconductance Amplifier (OTA) topologies in 180nm technology, comparing their gain-bandwidth-power-stability trade-offs.

## Overview

OTAs are foundational analog building blocks used in filters, data converters, and sensor interfaces. This project designs and characterizes two contrasting topologies to build intuition for topology selection under real design constraints:

- **Telescopic OTA** — single-stage cascode amplifier, optimized for speed and power efficiency
- **Two-Stage Miller-Compensated OTA** — two-stage amplifier with a Miller compensation capacitor, optimized for gain and stability

## Design Process

Both designs were hand-derived before simulation:
- Branch current allocation and overdrive voltage (Vov) budgeting across the stacked transistor network, accounting for the lower hole mobility in PMOS devices
- Aspect ratio (W/L) sizing derived from target overdrive voltages and current requirements
- Small-signal gain derivation via transconductance (gm) and output resistance (ro) of each stage — `Av = gm1,2 · [gm3·ro3·ro1 || gm5·ro5·ro7]`
- Initial hand-calculated gain (~1500 V/V) was below target; corrected by rescaling PMOS W/L while preserving aspect ratio, achieving ~3990 V/V

## Results

| Parameter | Telescopic OTA | Miller-Compensated OTA |
|---|---|---|
| Technology | 180nm CMOS | 180nm CMOS |
| Topology | Single-stage folded cascode | Two-stage with Miller compensation |
| DC Gain | ~20 dB (design) / 3990 V/V calculated | 54 dB (~501 V/V) |
| Unity Gain Bandwidth | 1.2 GHz | 5 MHz |
| Phase Margin | ~60° | >130° |
| Supply Voltage | ±1.8 V | ±1.8 V |
| Load Capacitance | 1 pF | 1 pF |
| Power Consumption | ~300 µW | <36 µW |

## Analysis & Conclusion

- **Bandwidth vs. gain trade-off:** the Telescopic OTA's single-stage cascode structure gives it a 240× bandwidth advantage (1.2 GHz vs. 5 MHz), but the Miller-Compensated OTA achieves far higher DC gain and phase margin due to its two-stage structure and compensation network.
- **Application fit:** Telescopic OTA is suited to high-speed, low-power applications — RF front-ends, high-speed ADCs, sample-and-hold circuits. The Miller OTA is suited to precision, high-gain applications — sensor interfaces, switched-capacitor filters, and systems with large capacitive loads requiring guaranteed stability.
- Frequency response (gain/phase) was simulated for both topologies and matched design targets within expected tolerance.

## Repository Contents

- `report/` — IEEE-format comparative study report
- `slides/` — Design presentation covering circuit diagrams, working principle (differential input, current steering, cascoding for gain boost), and derivations

## Authors

Karthik K Prasad, Advaith Shankar Bhat, M B Nishanth Aiyappa, Daivik I Vinayaka — Dept. of Electronics & Communication Engineering, The National Institute of Engineering, Mysuru
