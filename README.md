
# Discrete-Time Folded-Cascode OpAmp Design

Design and simulation of a fully differential folded-cascode operational amplifier in 0.18 µm CMOS, completed as the final project of EE4520 Analog CMOS Design 1 at TU Delft (MSc Microelectronics, 2025-2026).

## Project Overview

The amplifier is intended for discrete-time applications and is placed in a closed-loop feedback configuration with a target gain of 8 (≈ 18 dB). The core uses ideal gain-boosting blocks and an ideal common-mode feedback (CMFB), implemented as voltage-controlled voltage sources, so that the focus remains on the folded-cascode core itself. The cascode bias circuit was designed in a preparatory homework and reused here.

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

Final grade: 8.5/10

## What I Did

- Designed the cascode bias circuit (sizing of the NMOS and PMOS branches, choice of bias current ratios) to keep all cascode devices safely in saturation with Vgt ≈ 100 mV
- Built the full folded-cascode opamp with ideal gain-boosting and CMFB on top of the bias block
- Performed transient (step-response), AC (open-loop and closed-loop) and noise simulations in LTspice
- Iteratively optimized bias currents, transistor sizing and capacitor values to minimize power while satisfying all settling and noise specifications
- Analyzed key tradeoffs (gm vs DC gain, input pair sizing vs noise, global scaling vs noise spectrum, cascode bias balance vs output resistance) and documented the design methodology

## Repository Contents

- `report/` — final report submitted for EE4520, including the table of results, annotated schematics, all plots and the design methodology
- `schematics/` — annotated schematics with node voltages and branch currents
- `ltspice/` — LTspice simulation files:
  - `noise` — output noise spectral density simulation, integrated from 10 kHz to 100 GHz
  - `A_AB` — open-loop gain A and loop gain Aβ Bode plots (gain and phase), plus the closed-loop transfer function for the -3 dB bandwidth
  - `settling` — transient step-response simulation used to extract Tsettle, T40dB and T48.69dB

## Tools and Technology

- LTspice (0.18 µm CMOS process, custom parameter set without 1/f noise model as specified by the assignment)
- Supply: 1.8 V (separate supply for the bias block to isolate its power consumption from the FoM)

## Course

EE4520 Analog CMOS Design 1, TU Delft, MSc Microelectronics, 2025-2026
