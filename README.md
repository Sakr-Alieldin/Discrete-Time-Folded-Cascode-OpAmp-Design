# Discrete-Time Folded-Cascode OpAmp Design

Design and simulation of a fully differential folded-cascode operational amplifier in 0.18 µm CMOS, completed as the final project of EE4520 Analog CMOS Design 1 at TU Delft (MSc Microelectronics, 2025-2026), final grade 8.5/10.

## Project Overview

The amplifier is intended for discrete-time applications and is placed in a closed-loop feedback configuration with a target gain of 8 (≈ 18 dB). The core uses ideal gain-boosting blocks and ideal common-mode feedback (CMFB), with biasing provided by a separately designed cascode bias circuit.

The goal was to meet a set of individually assigned specifications (settling accuracy, settling time, SNR) at the lowest possible power dissipation, captured by a Figure-of-Merit:

```
FoM[dB] = -10 · log10(2π · Power · T_8.6dB / SNR²)
```

where T_8.6dB ≈ τcl (the closed-loop time constant), making the FoM independent of the specific settling accuracy each student was assigned.

## Results

| Parameter             | Spec       | Achieved     |
|-----------------------|------------|--------------|
| Closed-loop gain      | 8          | 8            |
| SNR                   | 68.53 dB   | 68.62 dB     |
| Settling accuracy     | 54 dB      | 54 dB        |
| Settling time         | 0.56 µs    | 0.559 µs     |
| Power dissipation     | minimum    | 22.1 µW      |
| Figure-of-Merit       | ≥ 174 dB   | 175.95 dB    |

## What I Did

- Designed the cascode bias circuit (sizing of the NMOS and PMOS branches, choice of bias current ratios) to keep all cascode devices safely in saturation with Vgt ≈ 100 mV
- Built the full folded-cascode opamp with ideal gain-boosting and CMFB on top of the bias block
- Performed transient (step-response), AC (open-loop and closed-loop) and noise simulations in LTspice
- Iteratively optimized bias currents, transistor sizing and capacitor values to minimize power while satisfying all settling and noise specifications
- Analyzed key tradeoffs and documented the design methodology, explaining the reasoning behind each design choice

## Repository Contents

### Report & Documentation
- **[Final Report](final_report.pdf)** — Complete project report with design methodology, results, and performance analysis
- **[Project Instructions](Project_instructions.pdf)** — Original assignment specifications and requirements

### LTspice Simulation Files
- **[Settling Response Simulation](CMOS1_HW2_setteling.asc)** — Transient step-response simulation
  - Used to extract Tsettle, T40dB and T48.69dB metrics
  - Closed-loop settling behavior verification

- **[AC Analysis & Frequency Response](CMOS_1_HW2_A_AB.asc)** — Bode plot simulations
  - Open-loop gain (A) and loop gain (Aβ) analysis
  - Closed-loop transfer function and -3 dB bandwidth verification

- **[Noise Spectral Density](CMOS_1_HW2_noise.asc)** — Noise simulation
  - Output noise spectral density analysis
  - Integrated noise from 10 kHz to 100 GHz
  - SNR extraction and verification

## Tools and Technology

- **Simulator:** LTspice
- **Process:** 0.18 µm CMOS (custom parameter set without 1/f noise model as per assignment specifications)
- **Supply Voltage:** 1.8 V (separate supply for bias block to isolate power consumption from FoM calculation)

## Course Information

**Course:** EE4520 Analog CMOS Design 1  
**Institution:** TU Delft, MSc Microelectronics  
**Academic Year:** 2025-2026  
**Grade:** 8.5/10
