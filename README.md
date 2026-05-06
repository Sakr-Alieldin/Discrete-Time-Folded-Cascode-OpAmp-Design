# Discrete-Time Folded-Cascode OpAmp Design

Design and simulation of a fully differential folded-cascode operational amplifier in 0.18 µm CMOS, completed as the final project of EE4520 Analog CMOS Design 1 at TU Delft (MSc Microelectronics, 2025-2026).

## Project Overview

The amplifier is intended for discrete-time applications and is placed in a closed-loop feedback configuration with a target gain of 8 (≈ 18 dB). The core uses ideal gain-boosting blocks and an input-pair cascode bias circuit with CMFB.

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

### Report & Documentation
- **[Final Report](report/)** — final report submitted for EE4520
  - Table of results and specifications
  - Design methodology and optimization process
  - Performance analysis and key design tradeoffs
  - Annotated schematics with node voltages and branch currents
  - Complete set of simulation plots (transient, AC, noise)
  
### Schematics
- **[Schematics Directory](schematics/)** — Circuit design files with detailed annotations
  - Full folded-cascode opamp with gain-boosting
  - Cascode bias circuit and CMFB
  - Node voltage labels and branch currents for verification
  - High-resolution images for documentation

### LTspice Simulations
- **[LTspice Directory](ltspice/)** — All simulation files and netlists
  - **`noise/`** — Output noise spectral density simulation
    - Integrated noise from 10 kHz to 100 GHz
    - SNR extraction and verification
  - **`A_AB/`** — AC analysis and frequency response
    - Open-loop gain (A) Bode plot
    - Loop gain (Aβ) analysis
    - Closed-loop transfer function and -3 dB bandwidth verification
  - **`settling/`** — Transient step-response simulations
    - Closed-loop settling behavior
    - Extraction of Tsettle, T40dB, and T48.69dB metrics
    - Accuracy vs. time validation

## Tools and Technology

- **Simulator:** LTspice
- **Process:** 0.18 µm CMOS (custom parameter set without 1/f noise model as per assignment specifications)
- **Supply Voltage:** 1.8 V (separate supply for bias block to isolate power consumption from FoM calculation)
- **Design Methodology:** Iterative optimization with performance-to-power tradeoff analysis

## Design Highlights

- **Gain-Boosting:** Ideal gain-boosting blocks implemented for improved DC gain while maintaining stability
- **Bias Circuit:** Carefully designed cascode bias with Vgt ≈ 100 mV to ensure all devices operate in saturation
- **CMFB:** Common-mode feedback circuit for fully differential architecture stability
- **Power Optimization:** Achieved 175.95 dB FoM through systematic transistor sizing and bias current optimization
- **Settling Performance:** 54 dB accuracy achieved in 559 ns at minimal power (22.1 µW)

## Specifications Met

✓ SNR: 68.62 dB (spec: 68.53 dB)  
✓ Settling Time: 559 ns (spec: 560 ns)  
✓ Settling Accuracy: 54 dB (spec: 54 dB)  
✓ Power Dissipation: 22.1 µW (minimized)  
✓ Figure-of-Merit: 175.95 dB (spec: ≥ 174 dB)

## Course Information

**Course:** EE4520 Analog CMOS Design 1  
**Institution:** TU Delft, MSc Microelectronics  
**Academic Year:** 2025-2026  
**Grade:** 8.5/10
